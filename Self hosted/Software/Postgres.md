Для pgAdmin добавить прав для 5050
```sh
ls -l /opt/postgres/pgadmin
sudo chown -R 5050:5050 /opt/postgres/pgadmin
```
docker-compose.yaml
```yaml
version: '3.5'

services:
  postgres:
    container_name: postgres_container
    image: postgres
    environment:
      POSTGRES_DB: ${POSTGRES_DB:-postgres}
      POSTGRES_USER: ${POSTGRES_USER:-postgres}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-MYPASPG}

    volumes:
       - /opt/postgres/postgres-data:/var/lib/postgresql/data
    ports:
      - "5432:5432"
    networks:
      - postgres
    restart: unless-stopped
  
  pgadmin:
    container_name: pgadmin_container
    image: dpage/pgadmin4
    environment:
      PGADMIN_DEFAULT_EMAIL: ${PGADMIN_DEFAULT_EMAIL:-MYEMAIL}
      PGADMIN_DEFAULT_PASSWORD: ${PGADMIN_DEFAULT_PASSWORD:-MYPAS}
      PGADMIN_CONFIG_SERVER_MODE: 'False'
    volumes:
       - /opt/postgres/pgadmin:/var/lib/pgadmin

    ports:
      - "${PGADMIN_PORT:-5050}:80"
    networks:
      - postgres
    restart: unless-stopped

networks:
  postgres:
    name: postgres-net
    driver: bridge
```

Заменить `MYPASPG`, `MYEMAIL`, `MYPAS` в docker-compose.yaml

#### Настройка pgAdmin
Servers =>  Register => Server
General => Name => PostgreSQL
Connection => 
Host name/address = postgres 
Port = 5432
Username = postgres
Password = pass

Save

#### Ссылки: 
1) [Запускаем PostgreSQL в Docker: от простого к сложному](https://habr.com/ru/articles/578744/)
2) [docker-compose.yaml](https://github.com/mfvanek/useful-sql-scripts/blob/master/running_pg_in_docker/3.%20Where%20is%20my%20data/docker-compose.yml)