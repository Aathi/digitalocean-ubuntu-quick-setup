### Configure PostgreSQL to allow remote connection


<!-- How  to check postgress running port -->
#### How to check PostgreSQL running port ?
```
$ netstat -nlt
```
or 
```
$ sudo netstat -plunt |grep postgres
```

<!-- Try to connect the Postgres via telnet to get to know about whether remote conection is configuerd or not -->
#### Try to connect the PostgreSQL via telnet to get to know about whether remote conection is configuerd or not
```
$ telnet 107.170.11.79 5432
```

#### if you see this you don't need to configure anything 
<!--  if you see this conf is exist-->
```
Trying 178.62.90.161...
Connected to 178.62.90.161.
Escape character is '^]'.
```

#### if you see this configuration need to be made
<!--  if you see this connection need to be made -->
```
Trying 107.170.11.79...
telnet: connect to address 107.170.11.79: Connection refused
telnet: Unable to connect to remote host
```

#### Configuring postgresql.conf
<!--  1. Configuring postgresql.conf -->
```
$ locate postgresql.conf
```

```
/etc/postgresql/9.5/main/postgresql.conf
/usr/lib/tmpfiles.d/postgresql.conf
/usr/share/postgresql/9.5/postgresql.conf.sample
```

#### Edit Configuring postgresql.conf
```
$ nano /etc/postgresql/9.5/main/postgresql.conf
```

<!-- replace line   -->
#### Replace line 
```
#listen_addresses = 'localhost' 
```
to this
```
listen_addresses = '*'
```

#### Now restart postgresql server
<!--  Now restart postgresql server -->
```
$ /etc/init.d/postgresql restart
```

#### Configuring pg_hba.conf
<!-- 2. Configuring pg_hba.conf  -->
```
$ locate pg_hba.conf
/etc/postgresql/9.5/main/pg_hba.conf
/usr/share/postgresql/9.5/pg_hba.conf.sample
```

#### Edit Configuring pg_hba.conf
```
$ nano /etc/postgresql/9.5/main/pg_hba.conf
```

```
#local   replication     postgres                                peer
#host    replication     postgres        127.0.0.1/32            md5
#host    replication     postgres        ::1/128                 md5
<!-- Add this line -->
 host    all             all             0.0.0.0/0               md5
 ```

#### Now restart postgresql server
<!--  Now restart postgresql server -->
```
$ /etc/init.d/postgresql restart
```


### Ref
1. https://blog.bigbinary.com/2016/01/23/configure-postgresql-to-allow-remote-connection.html
2. https://www.youtube.com/watch?v=eQiwvDkl7Qw

