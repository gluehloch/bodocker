Disclaimer: This site is under heavy construction/elaboration/etc./etc.

# PULL The Image

Does not work anymore:
```
docker pull mariadb/latest
```

That´s the way you do it:
```
docker run --net betoffice -p 3306:3306  --name mariadb -e MYSQL_ALLOW_EMPTY_PASSWORD=true -d mariadb:latest
```

## Build an image
```
docker build .
docker build . -t betoffice/botomcat:1.3.0-SNAPSHOT
```
## Run the image
```
docker run --net betoffice --expose 127.0.0.1:8080:8080 betoffice/botomcat:1.3.0-SNAPSHOT 
```

# TAG you image

https://docs.docker.com/engine/getstarted/step_six/
docker images

```
docker tag <imageid> <your-image-id>
docker tag <imageid> betoffice/mariadb:latest
docker tag 7d9495d03763 maryatdocker/docker-whale:latest
```

# Run the image

    ACHTUNG: Die IP Adresse ist anzupassen. So werden die Ports nur auf LOCALHOST freigeschaltet. Je nach dem wo die Docker-Machine läuft.

```
docker run --name bodata -p 127.0.0.1:3306:3306
    -e MYSQL_ALLOW_EMPTY_PASSWORD=true -d mariadb:latest
```

### botomcat-1.1.0

-- Nach Vorbereitung des Images, commit ...
-- Die Adresse 127.0.0.1 ist nicht korrekt, wenn die Instanz von 'außen' erreichbar sein soll.
-- Besser ist die IP Adresse des Containers: Also z.B. 192.168.99.100


### Config the MariaDB

docker exec -it mariadbtest bash

* Install the editor *

Auf der Bash in dem Docker Container arbeiten:

docker exec --it testtest bash

==> Per command line
```
apt-get update
apt-get install vim
```

==> Here with a docker file
```
FROM  confluent/postgres-bw:0.1

RUN ["apt-get", "update"]
RUN ["apt-get", "install", "-y", "vim"]
```

In der MariaDB Konfiguration müssen dann noch die folgenden Einstellungen vorgenommen werden.
Die folgenden Zeilen müssen kommentiert bleiben.
```
[mysqld]
    ...
    #skip-networking
    ...
    #bind-address = <some ip-address>
```

```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
```

```
************* MARIA DB Anpassungen *****************************
innodb_buffer_pool_size = 64M
innodb_additional_mem_pool_size = 12M
## Set .._log_file_size to 25 % of buffer pool size
innodb_log_file_size = 20M
innodb_log_buffer_size = 32M
# awi innodb_flush_log_at_trx_commit = 1
innodb_flush_log_at_trx_commit = 2

# awi
# A value of 1 is required for ACID compliance. You can achieve better performance
# by setting the value different from 1, but then you can lose at most one second
# worth of transactions in a crash. With a # value of 0, any mysqld process crash
# can erase the last second of transactions. With a value of 2, then only an
# operating system crash or a power outage can erase the last second of transactions.
# However, #InnoDB's crash recovery is not affected and thus crash recovery does work regardless of the value.


*********** Still performance issues ***************
betoffice-storage build--time 16 Minuten mit allen tests.

I tried:
innodb_buffer_pool_size = 256M => innodb_buffer_pool_size = 514M
```