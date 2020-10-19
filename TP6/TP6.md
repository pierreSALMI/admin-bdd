# TP6

1. [docker-compose.yml](docker-compose.yml)
2. [master](master.cnf) / [slave](slave.cnf)
3. [script](script.sql)
4. On dump la base de données du master `mysqldump -uroot -ppassword -A > backup/.dumpall.sql`
5. ```
    MariaDB [(none)]> show master status;
    +----------------------+----------+--------------+------------------+
    | File                 | Position | Binlog_Do_DB | Binlog_Ignore_DB |
    +----------------------+----------+--------------+------------------+
    | maria-db1-bin.000003 |     2110 |              |                  |
    +----------------------+----------+--------------+------------------+
    1 row in set (0.000 sec)
    ```
6. `CHANGE MASTER TO MASTER_HOST='maria-db1', MASTER_USER='replicant', MASTER_PASSWORD='replicant_password', MASTER_PORT=3306, MASTER_LOG_FILE='maria-db1-bin.000003', MASTER_LOG_POS=2110, MASTER_CONNECT_RETRY=10;` 
7. `START SLAVE;`
8.  Avant
    ```
        MariaDB [(none)]> show databases;
        +--------------------+
        | Database           |
        +--------------------+
        | aled               |
        | information_schema |
        | mysql              |
        | performance_schema |
        +--------------------+
        4 rows in set (0.001 sec)
    ```
    Apres
    ```
        MariaDB [(none)]> show databases;
        +--------------------+
        | Database           |
        +--------------------+
        | aled               |
        | information_schema |
        | mysql              |
        | nouvelle_base      |
        | performance_schema |
        +--------------------+
        5 rows in set (0.001 sec)
    ```