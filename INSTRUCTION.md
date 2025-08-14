## 1. Build and Push Django Application Image

Build the Django image using your standard `Dockerfile`:

docker build -t demon9709/volumes:1.0.1 .
docker push demon9709/volumes:1.0.1

text

---

## 2. Run MySQL Container with Volume

Create a Docker volume and run the MySQL container with persistent data storage:

docker volume create mysql_data

docker run -d
--name mysql-local
-e MYSQL_ROOT_PASSWORD=1234
-e MYSQL_DATABASE=app_db
-e MYSQL_USER=app_user
-e MYSQL_PASSWORD=1234
-v mysql_data:/var/lib/mysql
-p 3306:3306
mysql:latest

text

---

## 3. Run Django Application Container Connected to MySQL

Make sure the MySQL container (`mysql-local`) is running before starting the app container.

docker run -d
--name todoapp
--link mysql-local:mysql
-e DB_HOST=mysql-local
-e DB_USER=app_user
-e DB_PASSWORD=1234
-e DB_NAME=app_db
-p 8080:8080
demon9709/volumes:1.0.1

text

The application will be available on port `8080`.

---

## 4. Access the Application via Browser

Open your browser and navigate to:

http://localhost:8080

text

You should see the Django application running.

---

## 5. Docker Hub Repository Link

Django app image:  
https://hub.docker.com/repository/docker/demon9709/volumes/tags/1.0.1/sha256-73b1ba2298c3a6dac6f89c2d1150a634a67c0655b4e5fc756a9f65969c23ee7c