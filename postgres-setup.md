## Installing a PsyCopg2

Credential for exmple
```
host: localhost
port: 5433
username: postgres
password: 12345678
database_name: postgres
```

## Install pgadmin 
```bash
py -m venv myvenv
myvenv\Scripts\activate.bat
pip install psycopg2 psycopg2-binary
docker run --name my-postgres -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=12345678 -e POSTGRES_DB=postgres -p 5433:5432 -d postgres
 ```

## Setting in setting.py
To connect your Django project to a PostgreSQL database instead of SQLite,   you need to modify the `DATABASE` setting in your `settings.py` file.

Here's how you can do it
```py
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": "postgres",
        "USER": "postgres",
        "PASSWORD": "12345678",
        "HOST": "localhost",
        "PORT": "5433",
    }
}
```

## Setup with Docker Compose file
This is environment file you can follow this step

**.env**
```env
DB_USERNAME=postgres
DB_PASSWORD=password
DB_DATABASE=postgres
```
---
**docker-compose.yml**
```yml
version: "3"
services:
  django-db:
    container_name: django-db
    restart: always
    image: postgres:13-alpine # use latest official postgres version
    env_file:
      - .env
    environment:
      POSTGRES_USER: ${DB_USERNAME} # configure postgres
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DATABASE: ${DB_DATABASE}
    volumes:
      - database-data:/var/lib/postgresql/data/ # persist data even if container shuts down
    expose:
      - 5432
    ports:
      - 5432:5432
    command: -p 5432
    networks:
      - network

volumes:
  database-data: # named volumes can be managed easier using docker-compose
    driver: local
networks:
  network:
    driver: bridge
```

To execute build docker compose up, Please follow this step
```bash
docker-compose up -d --build
```