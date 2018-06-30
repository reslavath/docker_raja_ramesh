# docker_raja_ramesh


•	Session-1


Start the postgres container 
docker run -d  --name ramesh_pg -e POSTGRES_PASSWORD=mysecretpassword postgres

connect to the postgresql container using psql
docker run -it --rm --link ramesh_pg:postgres postgres psql -h postgres -U postgres
Password for user postgres:
psql (10.4 (Debian 10.4-2.pgdg90+1))
Type "help" for help.

postgres=#
        Is the server running locally and accepting
                                
                                
OR
connect to the container using bash

[node1] (local) root@192.168.0.48 ~
$ docker container ls
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
ce2cf2f05f04        postgres            "docker-entrypoint.s…"   8 minutes ago       Up 8 minutes        5432/tcp            ramesh_pg
bc8ff3bc1987        postgres            "docker-entrypoint.s…"   22 minutes ago      Up 22 minutes       5432/tcp            some-postgres
[node1] (local) root@192.168.0.48 ~

[node1] (local) root@192.168.0.48 ~
$ docker exec -it ramesh_pg bash
root@ce2cf2f05f04:/#
root@ce2cf2f05f04:/#
root@ce2cf2f05f04:/# pwd
/
root@ce2cf2f05f04:/# psql -U postgres
psql (10.4 (Debian 10.4-2.pgdg90+1))
Type "help" for help.



session-2


git clone https://github.com/CentOS/CentOS-Dockerfiles.git
cd CentOS-Dockerfiles/postgres/centos7/

vi  Dockerfile

RUN yum -y update; yum clean all
RUN yum -y install sudo epel-release; yum clean all
RUN yum localinstall -y https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-centos10-10-2.noarch.rpm

RUN yum -y install postgresql-server postgresql postgresql-contrib supervisor pwgen; yum clean all
RUN yum -y install barman ; yum clean all
RUN yum -y install pg_top;
RUN yum install -y http://www.pgpool.net/yum/rpms/3.7/redhat/rhel-7-x86_64/pgpool-II-release-3.7-1.noarch.rpm ; yum clean all
RUN yum install -y   pgpool-II-pg95 pgpool-II-pg95-extensions
RUN yum install -y pgbadger
RUN yum install -y pgbouncer ;  yum clean all


$ docker build --rm -t ramnaik/postgresql .

Successfully built afacd14724d8
Successfully tagged ramnaik/postgresql:latest

[node1] (local) root@192.168.0.48 ~/CentOS-Dockerfiles/postgres/centos7
$ docker run --name=postgresql -d -p 5432:5432 ramnaik/postgresql
946b089c4d6406d2b008fb4c3e980f60fc29354ab0797bc306f6deddc68e19c4



$ docker container ls
CONTAINER ID        IMAGE                COMMAND                  CREATED             STATUS    PORTS                    NAMES
b4c756717784        ramnaik/postgresql   "/bin/bash /start_po…"   4 minutes ago       Up 4 minutes    0.0.0.0:5432->5432/tcp   postgresql
[node1] (local) root@192.168.0.43 ~/CentOS-Dockerfiles/postgres/centos7
$


$ docker exec  -it b4c756717784 bash
[root@b4c756717784 /]#





[root@b4c756717784 /]# which psql
/usr/bin/psql
[root@b4c756717784 /]# which pg_top
/usr/bin/pg_top
[root@b4c756717784 /]# which pgbouncer
/usr/bin/pgbouncer
[root@b4c756717784 /]# which barman
/usr/bin/barman
[root@b4c756717784 /]# which pgpool
/usr/bin/pgpool
[root@b4c756717784 /]#
[root@b4c756717784 /]#
 [root@b4c756717784 /]# sudo -u  postgres psql
psql (9.2.23)
Type "help" for help.

postgres=# create database test_123;
CREATE DATABASE
postgres=# \q
[root@b4c756717784 /]# sudo -u  postgres psql -c'\l'
                                  List of databases
   Name    |  Owner   | Encoding |   Collate   |    Ctype    |   Access privileges
-----------+----------+----------+-------------+-------------+-----------------------
 postgres  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
 template0 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres    +
           |          |          |             |             | postgres=CTc/postgres
 template1 | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 | =c/postgres    +
           |          |          |             |             | postgres=CTc/postgres
 test_123  | postgres | UTF8     | en_US.UTF-8 | en_US.UTF-8 |
(4 rows)





