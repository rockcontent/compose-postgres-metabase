# Dockerized Metabase with PostgreSQL backend

[Metabase](https://www.metabase.com/) is an open-source java-based software that enables users to analyse data from a range of data sources including relational databases (e.g. Postgresql, MySQL etc.), NoSql databases etc.

It can be quite helpful when one has a data science question that could easily be answered by data analysis.

By default, it stores application-specific data e.g. users, stored queries, configurations etc. on an H2 database on the same file system where it is installed.

However, it is difficult to retrieve this data once the application crushes (which it might do if you write a wrong sql query for it to run on your data). It is therefore usually better to have the application save the data in a postgreSQL database such that it recovers its original state after any crush.

## Technology used

| Technology | Usage |
| --- | --- |
|[Docker](https://docs.docker.com/) | metabase and postgres run in different Docker containers|
|[Docker Compose](https://docs.docker.com/compose/) | Docker compose netwroks the different Docker containers to allow them  work together as dependent services |
|[Metabase](https://www.metabase.com/)| SQL based Analysis and Visualization program for any database |
|[Postgres](https://www.postgresql.org/)| A database engine that stores relational data in a persistent way |

## How to run

This assumes the local machine is running on Ubuntu or macOS.

1. Ensure [Docker](https://docs.docker.com/get-docker/) is installed.
2. Ensure [Docker Compose](https://docs.docker.com/compose/install/) is installed on your system.
3. Clone this git repository

    ```bash
    git clone https://github.com/rockcontent/compose-postgres-metabase.git
    ```

4. Enter the compose-postgres-metabase folder

    ```bash
    cd compose-postgres-metabase
    ```

5. Copy `.env.sample` to `.env`.

    ```bash
    cp .env.sample .env
    ```

6. Update the environment variables `POSTGRES_PASSWORD`, `METABASE_PASSWORD`, `MB_DB_PASS` and save.

    ```bash
    # Add the password for the postgres user
    POSTGRES_PASSWORD=<put here the_password for the postgres user>
    # Add the password for the metabase user
    METABASE_PASSWORD=<put here the password for the metabase user>
    MB_DB_PASS=<put here the password for the metabase user>
    ```

7. Start the docker compose services

    ```bash
    docker compose up
    ```

8. Set up your metabase instance by visiting the [local metabase start URL](http://localhost:3000)
If you are on a server or changed the port in your `.env`, use `http://<server IP>:<MB_HOST_APP_PORT>`.

## Service - Port Mappings

| Service | Default Port | environment variable |
| --- | --- | --- |
| Metabase | 3000 | MB_HOST_APP_PORT |
| Postgres | 3010 | MB_HOST_DB_PORT |

## Acknowledgement

Configuration inspired by the [Beyond Jupyter](https://github.com/jgoerner/beyond-jupyter) talk by [Joshua Gorner](https://github.com/jgoerner).
