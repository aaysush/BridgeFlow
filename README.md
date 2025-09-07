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

### 1. Pull the MySQL Docker image

```bash
docker pull mysql:latest
```

### 2. Create a Docker network

```bash
docker network create flasksql
```

### 3. Run the MySQL container

```bash
docker run -d --name databasemysql \
  --network flasksql \
  -e MYSQL_ROOT_PASSWORD=rootpass \
  -p 3306:3306 \
  mysql:latest
```

### 4. Create a database inside MySQL

```bash
docker exec -it databasemysql mysql -uroot -prootpass -e "CREATE DATABASE mydb;"
```

### 5. Build the Flask app Docker image

```bash
docker build -t flask-app-image .
```

### 6. Run the Flask container

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

### 7. Verify containers and network

```bash
docker ps
docker network inspect flasksql
```

### 8. Access the app

Open your browser and go to:

```
http://localhost:5000
```

## Notes

* Flask app uses environment variables to connect to MySQL
* Database is created if it does not exist
* All containers are connected through the `flasksql` network

## License

This project is licensed under the **MIT License** – see the LICENSE file for details.

---

If you want, I can also **make an even shorter, super clean “cheat-sheet style” README** for copy-pasting commands easily. This is useful for a GitHub project that’s mostly about Docker commands. Do you want me to do that?

