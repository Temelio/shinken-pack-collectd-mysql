# shinken-pack-collectd-mysql

## Description

This Shinken monitoring pack is used to manage mysql services with our
standard deployment of Collectd.

We request Collectd data using unixsock plugin and collectd-nagios script from
collecd-utils package.

This pack depends to shinken-pack-collectd-base to work

## Objects

### Templates

#### Host templates

* collectd-mysql: Manage all default thresholds and values for services

### Services

| Service name                         | Description                 | Value specification                            | DS        | Consolidation | Warning variable | Critical variable | Duplicate_foreach variable |
|--------------------------------------|-----------------------------|------------------------------------------------|-----------|---------------|------------------|-------------------|----------------------------|
| Mysql - $KEY$ processes              | Check Mysql processes       | processes-$VALUE1$/ps_count                    | processes | none          | $VALUE2$         | $VALUE3$          | _mysql_processes           |
| Mysql - $KEY$                        | Check listening ports       | tcpconns-$VALUE1$-local/tcp_connections-LISTEN | value     | none          | $VALUE2$         | $VALUE3$          | _mysql_listen              |
| Mysql - $KEY$ DB - Locks waited      | Checks DB locks waited      | mysql-$KEY$/mysql_locks-waited                 | value     | none          | $VALUE1$         | $VALUE2$          | _mysql_databases           |
| Mysql - $KEY$ DB - Threads connected | Checks DB threads connected | mysql-$KEY$/threads-connected                  | value     | none          | $VALUE3$         | $VALUE4$          | _mysql_databases           |
| Mysql - $KEY$ DB - Threads running   | Checks DB threads running   | mysql-$KEY$/threads-running                    | value     | none          | $VALUE5$         | $VALUE6$          | _mysql_databases           |
| Mysql - $KEY$ DB - Qcache not cached | Checks DB Qcache not cached | mysql-$KEY$/cache_result-qcache-not_cached     | value     | none          | $VALUE7$         | $VALUE8$          | _mysql_databases           |
| Mysql - $KEY$ DB - Tmp write         | Checks DB tmp write         | mysql-$KEY$/mysql_handler-tmp_write            | value     | none          | $VALUE9$         | $VALUE10$         | _mysql_databases           |

## Default values

    _mysql_databases    mysql $(1)$$(1)$$(1:)$$(1:)$$(1:)$$(1:)$$(5)$$(10)$$(256)$$(512)$
    _mysql_processes    mysqld $(mysqld)$$(1:1)$$(1:1)$,mysqld_safe $(mysqld_safe)$$(1:1)$$(1:1)$
    _mysql_listen       Listen 3306 $(3306)$$(1:1)$$(1:1)$
