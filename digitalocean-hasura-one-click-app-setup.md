```
Edit Yml File
https://docs.hasura.io/1.0/graphql/manual/guides/deployment/digital-ocean-one-click.html#

Login In to
docker exec -it 81eabd191030  

Login  as postgress user
docker exec -it 81eabd191030  psql -U postgres

CREATE USER hasurapostgres WITH PASSWORD 'hasurapostgres';
CREATE DATABASE hasurapostgres;
GRANT ALL PRIVILEGES ON DATABASE hasurapostgres TO hasurapostgres;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO hasurapostgres;

ERROR:  permission denied to create extension "pgcrypto"
ALTER USER hasurapostgres WITH SUPERUSER;

Restart docker
docker-compose restart caddy 

Check logger inorder to fing the ERROR
docker-compose logs 
```

