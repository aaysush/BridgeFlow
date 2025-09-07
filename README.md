# BridgeFlow
FlaskDBoost is a containerized two-tier web application built with Flask and MySQL. It demonstrates how to run a web application and a database in separate Docker containers while connecting them through a custom Docker network.


make

Here’s a concise summary of the commands and steps you used for your **two-tier Flask + MySQL Docker project**, which you can put in a `README.md`:

---

### Project Setup Commands

1. **Run MySQL container**

```bash
docker run -d --name databasemysql -e MYSQL_ROOT_PASSWORD=rootpass -p 3306:3306 mysql:latest
```

2. **Create Docker network**

```bash
docker network create flasksql
```

3. **Connect MySQL container to network**

```bash
docker network connect flasksql databasemysql
```

4. **Create database inside MySQL container**

```bash
docker exec -it databasemysql mysql -uroot -prootpass -e "CREATE DATABASE mydb;"
```

5. **Build Flask app image**

```bash
docker build -t flask-app-image .
```

6. **Run Flask container on the same network**

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

7. **Check running containers**

```bash
docker ps
```

8. **Inspect network to see connected containers**

```bash
docker network inspect flasksql
```

9. **Check logs if Flask container fails**

```bash
docker logs flask-app
```

---

If you want, I can **write a full `README.md` for this project**, including **description, setup steps, and how to run it**, ready to paste into GitHub. Do you want me to do that?
