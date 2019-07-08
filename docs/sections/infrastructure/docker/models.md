# Models
<hr>
<br>

#### Python for Postgres/Postgis Dockerfile model
```dockerfile
FROM python:3.7-stretch
MAINTAINER ivan

ENV PYTHONUNBUFFERED 1

COPY ./requirements.txt /requirements.txt

RUN apt update && apt install postgresql-server-dev-all binutils libproj-dev gdal-bin -y

RUN pip install -r /requirements.txt

RUN mkdir /app
WORKDIR /app
COPY ./app /app

RUN adduser --no-create-home user
USER user

```

#### docker-compose.yml Model
```yaml
version: "3"

services:
  app:
    build:
      context: .
    container_name: colectivos-app
    ports:
      - "8000:8000"
    volumes:
      - ./app:/app
    command: sh -c "gunicorn project_core.wsgi:application -w 4 -b 0.0.0.0:8000 --reload"
    env_file:
      - ./vars.env
    depends_on:
      - db
    networks:
      - colectivos-network

  db:
    build:
      context: .
      dockerfile: Dockerfile-postgres
    container_name: colectivos-db
    ports:
      - "5433:5432"
    env_file:
      - ./vars.env
    networks:
      - colectivos-network

networks:
  colectivos-network:
    driver: bridge
```