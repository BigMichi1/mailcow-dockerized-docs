# Installation von netdata

## Netdata

```yaml
version: '3'
services:
  netdata:
    image: netdata/netdata
    container_name: netdata
    pid: host
    network_mode: host
    restart: unless-stopped
    cap_add:
      - SYS_PTRACE
      - SYS_ADMIN
    security_opt:
      - apparmor:unconfined
    volumes:
      - netdataconfig:/etc/netdata
      - netdatalib:/var/lib/netdata
      - netdatacache:/var/cache/netdata
      - /:/host/root:ro,rslave
      - /etc/passwd:/host/etc/passwd:ro
      - /etc/group:/host/etc/group:ro
      - /etc/localtime:/etc/localtime:ro
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /etc/os-release:/host/etc/os-release:ro
      - /var/log:/host/var/log:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro

volumes:
  netdataconfig:
  netdatalib:
  netdatacache:
```

## MYSQL

```bash
docker-compose exec mysql-mailcow mysql -uroot -p${DBROOT} ${DBNAME}
```

```sql
CREATE USER 'netdata'@'172.22.1.1';
GRANT USAGE, REPLICATION CLIENT, PROCESS ON *.* TO 'netdata'@'172.22.1.1';
FLUSH PRIVILEGES;
```
