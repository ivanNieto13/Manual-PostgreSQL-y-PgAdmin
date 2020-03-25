# Desplegar contenedor de Postgres y Pgadmin

## docker-compose.yml
Guardar el contenido en un archivo nombrado `docker-compose.yml`

    version: '3.5'

    services:
    postgres:
        container_name: postgres_container
        image: postgres
        environment:
        POSTGRES_USER: ${POSTGRES_USER:-defaultuser}
        POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-changeme}
        PGDATA: /data/postgres
        volumes:
        - postgres:/data/postgres
        ports:
        - "5432:5432"
        networks:
        - postgres
        restart: unless-stopped

    pgadmin:
        container_name: pgadmin_container
        image: dpage/pgadmin4
        environment:
        PGADMIN_DEFAULT_EMAIL: ${PGADMIN_DEFAULT_EMAIL:-default@email.com}
        PGADMIN_DEFAULT_PASSWORD: ${PGADMIN_DEFAULT_PASSWORD:-changeme}
        volumes:
        - pgadmin:/root/.pgadmin
        ports:
        - "${PGADMIN_PORT:-5050}:80"
        networks:
        - postgres
        restart: unless-stopped

    networks:
    postgres:
        driver: bridge

    volumes:
        postgres:
        pgadmin:
Ejecutar en terminal:
```console
user@hostname:~$ docker-compose up -d
```

Esperar a que se descargue la imagen y se generen los contenedores.

## Nota: 
Es **importante cambiar** en el contenedor `postgres` los campos `POSTGRES_USER` y `POSTGRES_PASSWORD`.
Hacer lo mismo en el contenedor `pgadmin` los campos `PGADMIN_DEFAULT_EMAIL` y `PGADMIN_DEFAULT_PASSWORD`.