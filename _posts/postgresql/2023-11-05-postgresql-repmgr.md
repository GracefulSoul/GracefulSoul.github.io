---
title: "PostgreSQL REPMGR"
excerpt: "PostgreSQL의 REPMGR에 대한 설명과 사용 방법"
last_modified_at: 2023-11-05T15:30:00
header:
  image: /assets/images/postgresql/postgresql-repmgr.png
categories:
  - PostgreSQL
tags:
  - Programming
  - Database
  - PostgreSQL
  - REPMGR

toc: true
toc_ads: true
toc_sticky: true
---
# REPMGR[^REPMGR]
- PostgreSQL의 Replication 구성 방법 중 내부 설정만 사용하여 설정하는 방안도 있지만, PostgreSQL기반의 EnterpriseDB("EDB")에서 오픈소스로 개발 및 유지보수하는 REPMGR의 신뢰도와 다수 기능을 제공하는 REPMGR을 추천한다.

# SSH Setting
- Replication 구성 관리를 위한 SSH 설정을 구성하려는 모든 서버에서 수행해야 한다.
  - 우선 PostgreSQL 관리 계정인 postgres 계정으로 들어가 "/.ssh" 폴더를 만든다.
  - Password 인증을 사용하지 않기 위해 SSH RSA Public & Private Key 파일을 생성한다.
  - SSH 연결 시, 인증에 사용할 "authorized_keys" 파일에 자기 자신의 "id_rsa.pub" 파일 내용을 넣어주고, 해당 파일 권한을 600(rw-------)으로 변경한다.
```shell
su postgres
mkdir -p ~/.ssh
cd ~/.ssh
ssh-keygen -t rsa
cat id_rsa.pub >> authorized_keys
chmod 600 authorized_keys
```

- 모든 서버에 SSH key를 생성하였으면, 각 서버의 postgres 계정으로 SSH 접근하기 위한 다른 서버들의 SSH key를 가져와서 넣어주어야 한다.
  - 각 서버의 SSH 연결에 대한 SSH key를 "ssh-copy-id" 명령어를 이용하여 인증 후 가져온다.
  - 가져온 후 서버 도메인 정보가 맞게 적용되어 있는지 확인 후 수정한다.
  - 마지막으로 "restorecon" 명령어를 이용하여 설정을 서버에 적용한다.
```shell 
ssh-copy-id -p 22 postgres@{IP}
restorecon -Rv ~/.ssh
```

# Edit /etc/sudoers
- REPMGR에서 postgres 계정으로 관리자 명령어를 수행하기 위한 기본 권한 허용하기 위해서 "/etc/sudoers" 파일을 수정한다.
```shell
postgres ALL=NOPASSWD: /usr/bin/systemctl stop postgresql-12, \
/usr/bin/systemctl start postgresql-12, \
/usr/bin/systemctl restart postgresql-12, \
/usr/bin/systemctl reload postgresql-12, \
/usr/bin/systemctl stop repmgr12 \
/usr/bin/systemctl start repmgr12 \
/usr/bin/systemctl restart repmgr12 \
/usr/bin/systemctl reload repmgr12
```

# PostgreSQL
## Add repmgr user
- PostgreSQL Database 내 Replication 관리 계정과 Replication할 데이터베이스를 추가해야한다.
```shell
su postgres
createuser --superuser repmgr
createdb --owner=repmgr repmgr
```

- 기존 사용하는 계정과 DB가 존재하는 경우, 아래와 같이 해당 계정에 replication 권한만 부여하고 사용해도 된다.
```shell
ALTER USER gracefulsoul replication;
```

## PostgreSQL Setting
- PostgreSQL 설정 파일인 "postgresql.conf"에 아래 항목을 설정한다.
- "max_wal_senders"는 연결하려는 $Replication DB Count + 1$로 설정하면 된다.
```shell
listen_addresses = '*'
wal_level = replica
max_wal_senders = 3
wal_keep_segments = 8
archive_mode = on
archive_command = 'true'
shared_preload_libraries = 'repmgr'
```

- PostgreSQL 연결과 관련한 설정 파일인 "pg_hba.conf" 파일에 아래 항목을 추가한다.
- 기존 사용하던 계정과 DB가 존재하는 경우, 해당 계정과 DB로 설정해야한다.
```shell
local   replication     repmgr                                  trust
host    replication     repmgr          127.0.0.1/32            trust
host    replication     repmgr          10.0.2.1/24             trust
local   repmgr          repmgr                                  trust
host    repmgr          repmgr          127.0.0.1/32            trust
host    repmgr          repmgr          10.0.2.1/24             trust
```

# REPMGR
## REPMGR Install
- REPMGR의 기본적인 설치 방법은 공식 문서인 [Installing repmgr from packages](https://www.repmgr.org/docs/5.3/installation-packages.html){:target="_blank"}를 참조하는 것이 좋다.
- RPM을 받아 설치하고자 한다면, EDB의 [Public Repository](https://dl.enterprisedb.com/default/release/site/){:target="_blank"}에서 버전에 맞춰 다운로드후 rpm 설치를 수행한다.
```shell
rpm -Uvh repmgr12-5.3.0-1.el7.x86_64.rpm
```

## REPMGR Setting
- RPM을 설치하였다면 "/etc/repmgr/{PostgreSQLVersion}" 경로에 "repmgr.conf" 설정 파일을 수정해야한다.

```shell
node_id=1
node_name='primary'
conninfo='host=10.0.2.1 port=5432 dbname=repmgr user=repmgr'
data_directory='/var/lib/pgsql/12/data' 

#------------------------------------------------------------------------------
# Server settings
#------------------------------------------------------------------------------
config_directory='/var/lib/pgsql/12/data'

#------------------------------------------------------------------------------
# Replication settings
#------------------------------------------------------------------------------
replication_user='repmgr'
replication_type='physical'
use_replication_slots=yes

#------------------------------------------------------------------------------
# Logging settings
#------------------------------------------------------------------------------
log_level='ERROR'
log_file='/etc/repmgr/12/repmgr.log'

#------------------------------------------------------------------------------
# Event notification settings
#------------------------------------------------------------------------------
event_notification_command='/etc/repmgr/12/failover_promote.sh %n %e %d'
event_notifications='repmgrd_failover_promote'

#------------------------------------------------------------------------------
# Environment/command settings
#------------------------------------------------------------------------------
pg_bindir='/usr/pgsql-12/bin'
repmgr_bindir='/usr/pgsql-12/bin'

#------------------------------------------------------------------------------
# Failover and monitoring settings (repmgrd)
#------------------------------------------------------------------------------
failover='automatic'
reconnect_attempts=4
reconnect_interval=2
promote_command='/usr/pgsql-12/bin/repmgr standby promote -f /etc/repmgr/12/repmgr.conf --siblings-follow --log-to-file'
follow_command='/usr/pgsql-12/bin/repmgr standby follow -f /etc/repmgr/12/repmgr.conf --log-to-file --upstream-node-id=%n'
monitoring_history=yes
monitor_interval_secs=5

#------------------------------------------------------------------------------
# service control commands
#------------------------------------------------------------------------------
service_start_command='sudo systemctl start postgresql-12'
service_stop_command='sudo systemctl stop postgresql-12'
service_restart_command='sudo systemctl restart postgresql-12'
service_reload_command='sudo systemctl reload postgresql-12'
repmgrd_service_start_command='sudo systemctl start repmgr12'
repmgrd_service_stop_command='sudo systemctl stop repmgr12'
```

- 기존 사용하던 계정과 DB가 존재하는 경우, 각 설정마다 적용한 dbname과 user정보를 수정해주어야 한다.
- data_directory를 변경하였을 경우, 반드시 설정을 통해서 변경한 디렉토리로 설정하여야 한다.
- promote_command와 follow_command의 경우, 반드시 repmgr 파일의 절대 경로로 적용하여야 정상적인 커맨드 수행이 가능하다.
- "failover_promote.sh" 파일은 "failover" 설정이 "automatic"인 경우 사용할 파일로, 각자 구성에 맞추어 설정해야한다.
  - "%n" : 신규 Primary로 승격한 노드 번호
  - "%e" : Clustering 구조 내 발생한 이벤트 유형
  - "%d" : Clustering 구조 내 발생한 이벤트 상세 내용
  - "%e"가 "repmgrd_failover_promote"인 경우, 승격한 노드 번호와 죽은 노드 번호를 확인 가능하므로 "PostgreSQL Stop -> REPMGR Node Rejoin ->  PostgreSQL Start"를 스크립트로 만들면 클러스터링 구조의 빠른 복구가 가능하다.
- 저 외에도 다양한 설정들이 있으나, 글이 너무 길어질 수 있으므로 미사용 설정과 주석은 모두 삭제하였다.

## REPMGR service enable
- 최종 설정된 REPMGR service를 등록하여 서버 재시작에도 자동 실행되도록 설정한다.
```shell
systemctl enable repgmr12
```

# REPMGR Clustering
## primary DB Register
- 기존 사용하던 Database를 Primary로 등록한다.
```shell
/usr/pgsql-12/bin/repmgr primary register
/usr/pgsql-12/bin/repmgr cluster show
```

## stnadby DB Register
- 등록된 Primary DB를 clone하여 Standby DB를 구성한다.
```shell
# Remove all PostgreSQL's data
systemctl stop postgresql-12
rm -rf /var/lib/pgsql/12/data/*
# Clone
/usr/pgsql-12/bin/repmgr -h 10.0.2.1 -p 5432 -U repmgr -d repmgr standby clone
```
- 복제가 완료되면 Standby DB를 등록하고 시작한다.

```shell
systemctl start postgresql-12
systemctl start repmgr12
/usr/pgsql-12/bin/repmgr standby register
/usr/pgsql-12/bin/repmgr cluster show
```

# Failover
## Manual
- Standby DB 서버에서 "switchover" 명령어를 수행할 때, "--dry-run"을 통한 테스트 실행을 수행하여 정상적인 클러스터링 구조 설정이 되었는지 확인 후 수행한다.
```shell
/usr/pgsql-12/bin/repmgr standby switchover --siblings-follow --dry-run
```

## Automatic
- Primary DB를 강제종료할 때 설정된 "reconnect_interval"초마다 "reconnect_attempts"번 확인 후 "promote_command" 수행을 통해 Standby DB가 Primary로 승격하게 될 것이다.
- 단, 수행 이전에 Node Rejoin 커맨드를 만들어 놓고 수행하는 것이 좋다.
  - Replication의 Recovery Point를 벗어난 Node는 회복이 불가능하므로 재구성해야한다.
  - 위를 방지하기 위해 PostgreSQL 서버 설정 내 "max_wal_size"를 높히는 방법, 혹은 Backup 도구를 사용하는 방법 등이 존재한다.
```shell
systemctl stop postgresql-12
```

# Conclusion
- CPU나 Memory를 확장하여 Scale-up하는 방식의 확장이 불가능한 환경에서는 Replication 구성을 통해 Scale-out을 이용하여 구성하는 방법을 검토해야 한다.
- 구성이 다양해지고 Replication을 통해 역할이 분담이 될 때, 가장 고민하고 시간을 할애해야 하는 것은 해당 구성에 대한 테스트를 통한 안정성 확보이다.
- 데이터베이스는 서비스의 가장 중요한 부분으로, 장애가 발생하여 복구가 불가능한 최악의 상황에도 대처 가능하도록 백업 도구를 적극적으로 활용하는 것을 추천한다.

# Reference
[^REPMGR]: [repmgr 5.3.3 Documentation](https://www.repmgr.org/docs/5.3/index.html){:target="_blank"}