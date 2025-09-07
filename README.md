# BridgeFlow
FlaskDBoost is a containerized two-tier web application built with Flask and MySQL. It demonstrates how to run a web application and a database in separate Docker containers while connecting them through a custom Docker network.

---

## Features

* Flask web app with MySQL backend
* Dockerized environment for easy setup
* Uses a custom Docker network to connect containers
* REST API for inserting and viewing messages

## Prerequisites

* [Docker](https://www.docker.com/) installed
* Basic knowledge of Flask and MySQL

## Setup Instructions

1. Pull the MySQL Docker image

```bash
docker pull mysql:latest
```

2. **Run MySQL container**

```bash
docker run -d --name databasemysql -e MYSQL_ROOT_PASSWORD=rootpass -p 3306:3306 mysql:latest
```

3. **Create Docker network**

```bash
docker network create flasksql
```

4. **Connect MySQL container to network**

```bash
docker network connect flasksql databasemysql
```

5. **Create database inside MySQL container**

```bash
docker exec -it databasemysql mysql -uroot -prootpass -e "CREATE DATABASE mydb;"
```

6. **Build Flask app image**

```bash
docker build -t flask-app-image .
```

7. **Run Flask container on the same network**

```bash
docker run -d --name flask-app \
  --network flasksql \
  -e MYSQL_HOST=databasemysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=rootpass \
  -e MYSQL_DB=mydb \
  -p 5000:5000 \
  flask-app-image
```

8. **Check running containers**

```bash
docker ps
```

9. **Inspect network to see connected containers**

```bash
docker network inspect flasksql
```

10. **Check logs if Flask container fails**

```bash
docker logs flask-app
```


### Attach a volume



1. **Create a Docker Volume**

````bash
 
   docker volume create mysqldatavolume
````

2. **Verify the volume exists**

   ```bash
   docker volume ls
   ```

3. **Inspect the volume to see its location on the host**

   ```bash
   docker volume inspect mysqldatavolume
   ```
