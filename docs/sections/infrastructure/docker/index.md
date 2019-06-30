# Docker
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