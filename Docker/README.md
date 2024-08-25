## launch rds mysql db instance 

- login in cloudshell:
```sh
  mysql -h <endpoint_of_db_instance> -u <user_name> -p<password>
``` 
- create database in mysql 
```sh
CREATE DATABASE springbackend;
```
- exit from mysql
```sh
exit
```
- clone github repo 
```sh
git clone https://github.com/sharadrathod/angular.js_spring_boot_.with_Dockerfile.git 
```
- go into cloned repo
```sh
cd angular.js_spring_boot_.with_Dockerfile
``` 
- create shchema in mysql 
```sh
mysql -h <endpoint> -u <user> -p<password> springbackend < springbackend.sql 
```
Login to the database again:
```sh
mysql -h <endpoint> -u <user> -p<password> 
```
- View all the databases created:
  ```sh
  SHOW DATABASES;
  ```
  - Use the database:
  ```sh
  use springbackend;
  ```
  - View the tables created:
  ```sh
  SHOW tables;
  ```
  - View the content of the table:
  ```sh
  select * from tbl_workers;
  ``` 
  ## backend 

  - go into backend directory 
  ```sh
  cd backend
  ```
  - there is one file backend/application.properties
  ```sh
  vim application.properties
  ```
  - add there <endpoint of db>:3306
  - add user_name of=admin 
  - password=Admin123

  ## frontend 

  - cd into frontend 
  ```sh
  cd frontend 
  ```
  - edit worker.service.tf
  ```sh
  vim worker.service.tf
  ```
  - add public ip of instance and port we exposed 8085 

  ## Docker build

  ### backend 
  - cd into backend 
  ```sh
  cd backend 
  ```
  - **Docker build**
  ```sh
  docker build -t "piyu5233/angular-test:backend" .
  ```
  - **run and expose container**
  ```sh
  docker run -d -p 8085:8085 backend
  ```
  - check container 
  ```sh
  docker ps
  ```
  ### frontend 
  - cd into frontend
  - **Docker build**
  ```sh
  docker build -t "piyu5233/angular-test:frontend" .
  ```
  - **run and expose container**
  ```sh
  docker run -d -p 30080:30080 frontend
  ```
  - check container 
  ```sh
  docker ps
  ```
  - ***access page**
  ```sh
  public_ip_of_instance:30080/workers
  ```
  
