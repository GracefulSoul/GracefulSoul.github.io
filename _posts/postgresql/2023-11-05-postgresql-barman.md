---
title: "PostgreSQL Barman"
excerpt: "PostgreSQL의 Barman에 대한 설명과 사용 방법"
last_modified_at: 2023-11-06T16:30:00
header:
  image: /assets/images/postgresql/postgresql-barman.png
categories:
  - PostgreSQL
tags:
  - Programming
  - Database
  - PostgreSQL
  - Barman

toc: true
toc_ads: true
toc_sticky: true
---
# Barman[^Barman]
- PostgreSQL의 Replication 구성 이후 Recovery Point를 지나서 복구 불가능한 Standby 서버는 데이터를 삭제하고 다시 구성해야 한다.
- 이런 문제점을 해결하기 위한 방식 중 Backup 수단을 고려해야 하는데, 그 중 REPMGR과 연동이 수월하면서 PostgreSQL기반의 EnterpriseDB("EDB")에서 오픈소스로 개발 및 유지보수하는 Barman을 소개한다.

# Introduction
- 예기치 못한 상황에서 비즈니스의 연속성을 유지하기 위해서 필요한 도구를 제공한다.
- 대표적으로 비즈니스 연속성에는 아래의 두 항목이 0이 되는 이상적인 환경이 제공되기를 원한다.
  - Recovery Point Objective(RPO) : 중대한 사고로 인해 서비스에서 데이터가 손실될 수 있는 최대 목표 기간을 의미한다.
  - Recovery Time Objective(RTO) : 비즈니스 연속성 중단을 방지하기 위해서 서비스를 복구할 수 있는 목표 기간 및 서비스 수준을 의미한다.
- Barman은 위의 상황을 이상적으로 제공하기 위해서 사용하기 위한 백업 도구이다.

# Repmgr using Barman
- Rermgr 구성에 Barman 설정을 할 경우, 아래의 순서대로 진행하여야 한다.
  - Barman 서버 구성.
  - Primary 서버를 Barman 서버에 백업 후 concurrent_backup 수행.
  - Standby 서버의 Repmgr 설정 내 Barman 설정 후 "repmgr standby clone" 명령어 수행을 통해 Barman 연동.
  - Replication Cluster 구성 이후 "repmgr cluster show" 명령어를 사용하여 확인.
- Primary의 기본 데이터와 백업 주기에 설정된 데이터들을 기반으로 Replication Cluster 구성 및 Disaster Recovery가 가능한 구조로 설정이 된다.

# Requirement
- Linux/Unix
- Python >= 3.6
- Python modules:
  - argcomplete
  - psycopg2 >= 2.4.2
  - python-dateutil
  - setuptools
- PostgreSQL >= 10 (next version will require PostgreSQL >= 11)
- rsync >= 3.0.4 (optional)

# Install
- Barman 설치는 2ndquadrant Repository를 설정하여 yum으로 가능하며, 세부 사항은 [Document#Installation](https://docs.pgbarman.org/release/3.9.0/#installation){:target="_blank"} 섹션을 참고한다.
- compression 설정을 사용할 경우, 사용하려는 타입에 맞는 utility를 설치해야 한다. 
```shell
yum install barman
yum install gzip
```

## SSH Setting
- Barman과 연동하여 Backup과 Recovery를 수행하기 위해서 SSH 설정을 구성하려는 모든 서버에서 수행해야 한다.
  - 우선 PostgreSQL 관리 계정인 postgres 계정으로 들어가 "/.ssh" 폴더를 만든다.
  - Password 인증을 사용하지 않기 위해 SSH RSA Public & Private Key 파일을 생성한다.
  - SSH 연결 시, 인증에 사용할 "authorized_keys" 파일에 자기 자신의 "id_rsa.pub" 파일 내용을 넣어주고, 해당 파일 권한을 600(rw-------)으로 변경한다.
```shell
su barman
mkdir -p ~/.ssh
cd ~/.ssh
ssh-keygen -t rsa
cat id_rsa.pub >> authorized_keys
chmod 600 authorized_keys
```

- 모든 서버에 SSH key를 생성하였으면, 각 서버의 barman 계정으로 SSH 접근하기 위한 다른 서버들의 SSH key를 가져와서 넣어주어야 한다.
  - 각 서버의 SSH 연결에 대한 SSH key를 "ssh-copy-id" 명령어를 이용하여 인증 후 가져온다.
  - 가져온 후 서버 도메인 정보가 맞게 적용되어 있는지 확인 후 수정한다.
  - 마지막으로 "restorecon" 명령어를 이용하여 설정을 서버에 적용한다.
```shell 
ssh-copy-id -p 22 barman@{IP}
restorecon -Rv ~/.ssh
```

# Barman Configuration
- barman을 설치하면 barman 설정인 "/etc/barman/" 폴더 내 "barman.conf" 파일과 백업 데이터베이스 설정을 수행할 "conf.d" 폴더가 생성된다.
- 위에서 우선 "barman.conf" 설정을 수정한다.
```shell
[barman]
barman_user = barman
configuration_files_directory = /etc/barman/conf.d
barman_home = /var/lib/barman
log_file = /etc/barman/logs/barman.log
log_level = ERROR
compression = gzip
immediate_checkpoint = true
basebackup_retry_times = 3
retention_policy = RECOVERY WINDOW OF 1 WEEKS
```

- retention_policy는 백업 보관 기간을 설정하는 옵션으로, Repmgr 구성에서 오류가 발생하여 복구하기 위한 Recovery Point를 확장하기 위한 기간을 고려하여 설정하면 된다.

- 백업을 위한 Primary 서버의 설정 파일 "/etc/barman/conf.d/repmgr-primary-server.conf"을 만들어준다.

```shell
[primary]
description =  "Repmgr Primary Server"
 
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; SSH options (mandatory)
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
ssh_command = ssh postgres@10.0.2.1
 
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; PostgreSQL connection string (mandatory)
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
conninfo = host=10.0.2.1 port=5432 user=postgres dbname=repmgr
 
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; Backup settings (via rsync over SSH)
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
backup_method = rsync
reuse_backup = link
backup_options = concurrent_backup
parallel_jobs = 1
 
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; Continuous WAL archiving (via 'archive_command')
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
archiver = on
path_prefix = "/usr/pgsql-10/bin"
 
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; PostgreSQL streaming connection string
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
streaming_conninfo = host=10.0.2.1 port=5432 user=postgres dbname=repmgr
 
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; WAL streaming settings (via pg_receivewal)
; ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
streaming_archiver = on
slot_name = primary
create_slot = auto
```

- PostgreSQL 내 계정을 별도 생성하여 사용하지 않고 postgres 계정으로 명령 수행하도록 할 수 있다.
- 백업 방식은 공식 홈페이지의 [Document#Backup-and-Architecture](https://docs.pgbarman.org/release/3.9.0/#design-and-architecture){:target="_blank"} 섹션을 참고하여 설정을 변경한다.


# Install in PostgreSQL Server
## Barman-cli & rsync
- Barman 서버와 연동할 PostgreSQL 서버들에는 클라이언트 유틸리티인 barman-cli를 설치한다.
```shell
yum install barman-cli
```

- rsync 방식으로 Backup을 수행하는 경우, PostgreSQL 서버에도 rsnyc가 설치되어 있어야 한다.
```shell
yum install rsync
```

## PostgreSQL Configuration
- PostgreSQL 서버 내 PostgreSQL 설정에서 "postgresql.conf" 파일에 아래의 내용을 추가한다.
```shell
max_wal_senders = 3         # max number of walsender processes
                            # (change requires restart)
max_replication_slots = 3   # max number of replication slots
wal_level = replica         # minimal, replica, or logical
                            # (change requires restart)
archive_mode = on           # enables archiving; off, on, or always
                            # (change requires restart)
archive_command = 'rsync -a %p postgres@10.0.2.20:/var/lib/barman/primary/incoming/%f'
```

- PostgreSQL 서버 내 PostgreSQL 설정에서 "pg_hba.conf" 파일에 아래의 내용을 추가한다.
```shell
host    all     barman                  10.0.2.0/24        trust
host    all     streaming_barman        10.0.2.0/24        trust
```

## Repmgr Configuration
- Repmgr 설정 내 "/etc/repmgr/{POSTGRESQL_VERSION}/repmgr.conf" 파일에 Barman 서버 설정을 수행한다.
```shell
restore_command='/usr/bin/barman-wal-restore -U postgres 10.0.2.20 primary %f %p'

barman_host=barmanserver
barman_server=10.0.2.1
restore_command=/usr/bin/barman-wal-restore barmanserver 10.0.2.1 %f %p
```

# Clone
- Repmgr 구성 내 Primary 서버의 연동을 설정한다.
```shell
barman switch-wal --force --archive primary
barman cron
barman check primary
```

- "barman check {SERVER_NAME}" 명령어를 수행하여 OK가 되지 않는 항목은 각 설정을 수정하여 모두 정상화 시켜야된다.

# Backup
- Barman을 통해 임의 시점에서 설정된 "backup_method"의 방식으로 시스템 운영 중 백업 수행이 가능하다.
  - rsync/SSH의 경우 "ssh_command"의 설정을 활용된다.
```shell
barman backup primary
```

# Caution
- Barman을 구성할 때 주의 사항으로, 기본으로 생성하는 barman 계정을 그대로 사용해야한다.
- Rermgr 등 다른 시스템과 연동 설정을하다 보면 원인 파악이 어려운 다양한 오류가 발생할 수 있다.
  - 이 때 Linux 로그("/var/logs/*") 내 연동 요청에 대해서 "Permission denied" 혹은 "Failed"등의 오류를 참고한다.

# Conclusion
- 이 외에도 pgBackRest, WAL-E, pg_basebackup, 등을 이용한 백업 방안이 존재하므로 서비스 환경과 시스템 구성에 맞는 도구를 선택하는 것 또한 중요하다.
- 백업은 위에서 이야기한 RPO, RTO가 0이 되는 이상적인 비즈니스 연속성을 제공된 환경을 구성하기 위해 가장 중요한 수단이다.
- 서비스가 안정적으로 구성된다면 다양한 기능 개발, 시스템 안정성 확보, UX 설계 등을 기반으로 사용자의 만족도 증진에 집중할 수 있으므로 반드시 고려해보기를 바란다.

# Reference
[^Barman]: [Barman Home](https://pgbarman.org/){:target="_blank"}