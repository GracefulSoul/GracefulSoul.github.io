---
title: "PostgreSQL Pgpool-II"
excerpt: "PostgreSQL의 Pgpool에 대한 설명과 사용 방법"
last_modified_at: 2023-11-05T18:30:00
header:
  image: /assets/images/postgresql/postgresql-pgpool-ii.png
categories:
  - PostgreSQL
tags:
  - Programming
  - Database
  - PostgreSQL
  - Pgpool-II

toc: true
toc_ads: true
toc_sticky: true
---
# Pgpool-II[^Pgpool-II]
- PostgreSQL 서버 풀을 관리하는 도구로, 단일 PostgreSQL 구성에서 사용할 수 없는 다양한 기능을 제공한다.

# Features
## High Availability
- 여러 PostgreSQL 서버를 사용하여 HA 구성을 제공하며, 손상된 서버를 서버 풀에서 자동으로 제거하여 데이터베이스 작업을 계속 수행한다.
- Pgpool-II는 Watchdog이라는 Pgpool-II 자체에 대한 HA 기능도 제공하여 [Quorum Algorithm](https://en.wikipedia.org/wiki/Quorum_(distributed_computing)){:target="_blank"}을 사용하여 [Split-Brain](https://en.wikipedia.org/wiki/Split-brain_(computing)){:target="_blank"} 현상이 발생하지 않도록 지원한다.
## Load balancing
- 더 높은 성능을 얻기 위해서 여러 PostgreSQL 서버에 Read 쿼리를 분산시켜준다.
- Write 쿼리는 아래의 각 경우에 따라 해당 서버로 전달된다.
  - Streaming Replication 모드인 경우, Primary 서버에만 제공된다.
  - 그 외의 Native Replication 모드이거나 Snapshot Isolation 모드인 경우, 모든 서버로 분산시켜준다.
## Connection Pooling
- PostgreSQL 서버에 대해 설정된 연결을 유지하고 동일한 속성(user, database, protocol version, and other connection parameters)을 가진 새 연결이 들어올 때마다 이를 재 사용한다.
## Online Recovery
- 하나의 명령을 실행하여 데이터베이스 노드의 온라인 복구를 수행할 수 있다.
- 자동 장애 조치와 함께 온라인 복구를 사용하는 경우 장애 조치에 의해 분리된 노드를 자동으로 대기 노드로 연결하는 것이 가능하다.
- 새로운 PostgreSQL 서버를 동기화하고 연결하는 것도 가능하다.
## Limiting Exceeding Connections
- PostgreSQL의 최대 동시 연결 수에는 제한이 있으며, 최대 연결 수를 늘리면 리소스 소비가 증가하고 전체 시스템 성능에 부정적인 영향을 미칠 수 있으므로 제한에 도달하면 새 연결이 거부된다.
## Watchdog
- 여러 Pgpool-II를 연결하여 강력한 Cluster 시스템을 구성하며, 단일 실패 지점 또는 Split-Brain을 방지할 수 있습니다.
- Split-Brain을 방지하기 위해서는 최소 3개 이상의 Pgpool-II를 연결해야한다.
## In Memory Query Cache
- 한 쌍의 SELECT 문과 그 결과를 저장하여 동일한 SELECT가 들어오면 Pgpool-II는 캐시에서 값을 반환한다.
- SQL 구문 분석이나 PostgreSQL에 대한 액세스가 포함되지 않으므로 매우 빠르다. 

# Install
## libevent & libevent
- 위에서 이야기한 In Memory Query Cache 기능을 활용하므로 libevent와 libmemcached를 설치해야 pgpool을 설치 가능하다.
```shell
yum install libevent
yum install libevent
```

## Pgpool-II
- Pgpool 사이트 내 [Downloads](https://pgpool.net/mediawiki/index.php/Downloads){:target="_blank"} 페이지를 참고하여 Yum repository 설정이거나 RPM을 다운로드 받아 설치하면 된다.

## Pgpool-II Configuration
- Pgpool-II를 설치하면 "/etc/pgpool-II" 폴더 내 다양한 설정 파일이 존재한다.

### pgpool.conf
```shell
# ----------------------------
# pgPool-II configuration file
# ----------------------------
backend_clustering_mode = 'streaming_replication'
 
#------------------------------------------------------------------------------
# CONNECTIONS
#------------------------------------------------------------------------------
# - pgpool Connection Settings -
listen_addresses = '*'
port = 9999
socket_dir = '/tmp'
pcp_listen_addresses = '*'
pcp_port = 9898
pcp_socket_dir = '/tmp'

# - Backend Connection Settings -
backend_hostname0 = '10.0.2.1'
backend_port0 = 5432
backend_weight0 = 1
backend_data_directory0 = '/var/lib/pgsql/12/data'
backend_flag0 = 'ALWAYS_PRIMARY'
backend_application_name0 = 'master'
 
backend_hostname1 = '10.0.2.10'
backend_port1 = 5432
backend_weight1 = 1
backend_data_directory1 = '/var/lib/pgsql/12/data'
backend_flag1 = 'ALLOW_TO_FAILOVER'
backend_application_name1 = 'standby1'
 
backend_hostname2 = '10.0.2.20'
backend_port2 = 5432
backend_weight2 = 1
backend_data_directory2 = '/var/lib/pgsql/12/data'
backend_flag2 = 'ALLOW_TO_FAILOVER'
backend_application_name2 = 'standby2'

#------------------------------------------------------------------------------
# POOLS
#------------------------------------------------------------------------------
num_init_children = 100

#------------------------------------------------------------------------------
# FILE LOCATIONS
#------------------------------------------------------------------------------
pid_file_name = '/var/run/pgpool/pgpool.pid'
logdir = '/etc/pgpool-II/log'

#------------------------------------------------------------------------------
# LOAD BALANCING MODE
#------------------------------------------------------------------------------
load_balance_mode = on
ignore_leading_white_space = on
write_function_list = ''
database_redirect_preference_list = ''
app_name_redirect_preference_list = ''
allow_sql_comments = off
disable_load_balance_on_write = 'transaction'

#------------------------------------------------------------------------------
# STREAMING REPLICATION MODE
#------------------------------------------------------------------------------
# - Streaming -
sr_check_period = 10
sr_check_user = 'repmgr'
sr_check_password = 'repmgr'
sr_check_database = 'repmgr'
delay_threshold = 1000000
```

### pcp.conf
- pg_md5를 이용하여 패스워드를 암호화 하여 "username:[md5 encrypted password]" 형태로 넣어준다.
```shell
root:1060b7b46a3bd36b3a0d66e0127d0517
```

## Firewall
- 위에서 사용하는 9999 포트에 대해서 방화벽 설정을 추가 후 적용한다.
```shell
firewall-cmd --permanent --zone=public --add-port=9999/tcp
firewall-cmd --reload
```

# Service
- Pgpool-II 서비스를 등록 및 상태를 확인한다.
```shell
systemctl enable pgpool
systemctl start pgpool
systemctl status pgpool
```

# Node check
- psql 명령어로 Pgpool-II 서비스에 연결하여 pool에 연결된 node들의 상태를 확인한다.
```shell
psql -h localhost -p 9999 -U repmgr -d repmgr -c 'show pool_nodes;'
```

# Conclusion
- 단일 PostgreSQL을 사용하다 보면 부하 분산에 대한 다양한 구성을 고려하게된다.
- Repmgr에서 이야기하였듯이 Scale-up은 서비스 중단에 대한 리스크가 분명히 존재하므로 유연한 구성을 하기 위한 Scale-out 등 다양한 방법을 고려하여야 한다.
- 이러한 모든 작업은 개발과 동일하게 확장에 열려있도록 아키텍쳐를 구성하고 원활한 서비스를 제공하기 위한 기반 작업이다.
- 위에서 설명하였듯이 다양한 기능들이 Pgpool-II에 존재하지만, 이 글에서 작성한 단순 구성 설정 외 다양한 설정들을 이용하여 자신만의 서비스에 접목시키면 더 효율적인 서비스 운영이 될 것으로 판단된다.

# Reference
[^PGPool-II]: [PGPool-II Home](https://www.pgpool.net/mediawiki/index.php/Main_Page){:target="_blank"}