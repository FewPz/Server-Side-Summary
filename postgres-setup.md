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