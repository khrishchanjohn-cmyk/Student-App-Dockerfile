# Student-App-Dockerfile

---

##  Student Registration Website

This is a student registration web application used to register students who take admission in our institute.


---

##  Application Overview

App Name: Student Registration Website
Purpose: Register students online for institute admission.


---

##  Project Setup

 Frontend Requirements

Node.js installed

npm installed


 Backend Requirements

Java Development Kit (JDK) 17 or higher installed

Maven installed


🗄 Database Requirements

MariaDB installed



---

##  Infrastructure Prerequisites

Before setting up the application, ensure the following are ready:

✅ RDS is created (for MySQL database connection).

✅ EC2 instance is launched.

✅ Docker is installed.

✅ MySQL client is installed.



---

##  Setup Steps

1️ Switch to Root Directory
```sh
sudo -i
```
2️ Update the Instance
```sh
apt update
```
3️ Install Docker
```sh
apt install docker.io -y
```
4️ Install MySQL Client
```sh
apt install mysql-client -y

```

---

##  Clone the Repository
```sh
git clone <your-github-repository-link>

```
---

##  Backend Setup

Navigate to Backend Directory
```sh
cd <GitHub-repository-name>/backend
```
Configure application.properties
```sh
nano application.properties
```
Changes to make:

Replace localhost with your RDS endpoint.

Update database name, username, and password.



---

 Create Backend Dockerfile
```sh
nano Dockerfile
```
Paste the following content:
```sh
FROM maven:3.8.3-openjdk-17
COPY . /OPT
WORKDIR /OPT
RUN rm -rf src/main/resources/application.properties
RUN cp -rf application.properties src/main/resources
RUN mvn clean package
WORKDIR /OPT/target
EXPOSE 8080
CMD ["java", "-jar", "student-registration-backend-0.0.1-SNAPSHOT.jar"]
```

---

##  Build Docker Image
```sh
docker build . -t backend:v1
```
##  Run Docker Container
```sh
docker run -d -p 8080:8080 backend:v1
```
##  Verify Running Containers
```sh
docker ps

```
---

##  Frontend Setup

Navigate to Frontend Directory
```sh
cd <GitHub-repository-name>/frontend
```
##  Create Frontend Dockerfile
```sh
nano Dockerfile
```
Paste the following content:
```sh
FROM node:25-alpine3.21
COPY . /OPT
WORKDIR /OPT
RUN apk update -y
RUN apk add apache2
RUN npm install
RUN npm run build
RUN cp -rf dist/* /var/www/localhost/htdocs/
EXPOSE 80
CMD ["httpd", "-D", "FOREGROUND"]
```

---

##  Build Docker Image
```sh
docker build . -t frontend:v1
```
##  Run Docker Container
```sh
docker run -d -p 80:80 frontend:v1
```
##  Verify Running Containers
```sh
docker ps

```
---

 Summary

Component	Port	Image Name	Command

Backend	8080	backend:v1	docker run -d -p 8080:8080 backend:v1 

Frontend	80	frontend:v1	docker run -d -p 80:80 frontend:v1 



---

✅ Final Notes

Ensure the RDS endpoint is properly configured in the backend application.properties.

Access the website at your EC2 public IP (port 80).
```sh
http://<EC2-PUBLIC-IP>
```
The backend API runs on port 8080.



---
