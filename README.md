# Angular Springboot Project Deployment

This project demonstrates the deployment of an Angular frontend application and a Spring Boot backend application using Kubernetes. It includes the necessary YAML files for deployment and service configuration. Follow the instructions below to deploy and configure the applications.
- to download kubectl command 
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```
```
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```
```
chmod +x kubectl
mkdir -p ~/.local/bin
mv ./kubectl ~/.local/bin/kubectl
``` 
```
kubectl version --client
```
- to configure eks cluster 
```
aws eks update-kubeconfig --region us-east-1 --name my-cluster
```


## Table of Contents

- [Project Overview](#project-overview)
- [Prerequisites](#prerequisites)
- [Deployment Instructions](#deployment-instructions)
- [Service Configuration](#service-configuration)
- [Post-Deployment Configuration](#post-deployment-configuration)
- [Increasing Replicas](#increasing-replicas)

## Project Overview

This project involves deploying an Angular frontend application and a Spring Boot backend application in a Kubernetes cluster. The deployment files and service configurations are provided to ensure a smooth setup and running of the applications.

## Prerequisites

- Kubernetes cluster
- kubectl configured and connected to your cluster
- Docker images for frontend and backend applications
- Source code of the project

## Deployment Instructions

1. **Deploy the Backend Application**

- Apply the backend deployment 

```
kubectl apply -f backend-deployment.yaml
```
- service YAML files:
```
kubectl apply -f backend-service.yaml
```

## Deployment Instructions

2. **Deploy Frontend Application**

   Apply the frontend deployment and service YAML files:

```
kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml
```
## Post-Deployment Configuration

After deploying the applications, there are a few post-deployment configurations to perform:

### Updating Backend Service Endpoint in Frontend

The frontend application needs to communicate with the backend application. Therefore, you need to update the backend service endpoint in the frontend to the Node's public IP address. Follow these steps:

1. **Identify the Node's Public IP Address**

You can obtain the public IP address of your Kubernetes cluster's Node by running the following command:

```
kubectl get nodes -o wide
```
## Configuration

### Worker Service File for Frontend

To ensure proper communication between the frontend and backend, follow these steps:

1. **Modify `worker.service.ts` in the frontend directory of your project.**

2. **Replace the `backend-service` with your Node Public IP address.**

3. **Copy the file to the frontend application directory in the Kubernetes pod:**

```
kubectl cp worker.service.ts <frontend-pod-name>:/opt/angular-frontend/src/app/services/worker.service.ts
```
4. **Replace <frontend-pod-name> with the name of your frontend pod.**

### Application Properties for Backend

1. **Modify `application.properties` in the backend directory of your project.**

2. **Replace the `database-endpoint, username and password` with your own data.**

3. **Copy the file to the backend application directory in the Kubernetes pod:**

```
kubectl cp application.properties <backend-pod-name>:/opt/spring-backend/src/main/resources/application.properties
```
4. **Replace <backend-pod-name> with the name of your backend pod.**

### Example of modifying the file:

1. **Replace `<database-host>`, `<port>`, `<database-name>`, `<database-username>`, and `<database-password>` with your database configuration.**

```
spring.datasource.url=jdbc:mysql://<database-host>:<port>/<database-name>
spring.datasource.username=<database-username>
spring.datasource.password=<database-password>
```
## Scaling

To scale the application based on your requirements, you can adjust the number of replicas for the frontend and backend deployments.

### Scaling Frontend Deployment

To scale the frontend application, follow these steps:

1. **Determine the Current Number of Replicas**

   You can check the current number of replicas for the frontend deployment by running the following command:

```
kubectl get deployment frontend-app
```
2. **To Scale the deployments just open the yaml file and enter the desired number of replicas and apply the files.**


