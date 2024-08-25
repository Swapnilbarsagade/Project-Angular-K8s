## launch rds mysql db instance 

- login in :
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
git clone https://github.com/abhipraydhoble/Project-Angular-K8s.git
```
- go into cloned repo
```sh
cd Project-Angular-K8s
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
  - password=Pass1234%

  ## frontend 

  - cd into frontend 
  ```sh
  cd frontend 
  ```
  - edit worker.service.tf
  ```sh
  vim worker.service.tf
  ```
  - add public ip of instance and port we exposed 8081

  ## Docker build

  ### backend 
  - cd into backend 
  ```sh
  cd backend 
  ```
  - **Docker build**
  ```sh
  docker build -t ang-backend .
  ```
  - **run and expose container**
  ```sh
  docker run -d -p 8081:8081 ang-backend
  ```
  - check container 
  ```sh
  docker ps
  ```
  ### frontend 
  - cd into frontend
  - **Docker build**
  ```sh
  docker build -t ang-frontend .
  ```
  - **run and expose container**
  ```sh
  docker run -d -p 30080:30080 ang-frontend 
  ```
  - check container 
  ```sh
  docker ps
  ```
  - ***access page**
  ```sh
  public_ip_of_instance:30080/workers
  ```
  
