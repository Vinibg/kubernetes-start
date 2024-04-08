# Kubernetes Deployment with Nginx and MySQL

## Overview

This project provides a simple setup for running Nginx web server and MySQL database on Kubernetes. It aims to simulate a basic server and database environment for development or testing purposes.

## Features

- **Nginx Server**: Provides a web server environment for hosting static or dynamic content.
- **MySQL Database**: Offers a relational database management system for storing and managing data.

## Getting Started

### Prerequisites

- Kubernetes cluster set up (local or cloud-based). You can use Minikube for local development.
- `kubectl` command-line tool installed and configured to access your Kubernetes cluster.


### Deployment Mysql

1. Clone this repository:

    ```bash
    git clone https://github.com/your_username/kubernetes-nginx-mysql.git
    ```

2. Apply the Kubernetes manifests:

    ```bash
    cd mysql
    kubectl apply -f namespace.yaml
    kubectl -n mysql apply -f pvc.yaml
    kubectl -n mysql apply -f configmap.yaml
    kubectl -n mysql apply -f deployment.yaml
    kubectl -n mysql apply -f service.yaml
    
    ```

3. Verify the deployments:

    ```bash
    kubectl -n mysql get deployments
    kubectl -n mysql get pods
    kubectl -n mysql get svc
    kubectl -n mysql get pvc
    kubectl -n mysql get configmap
    ```

### Deployment Nginx

1. Go to nginx directory
    ```bash
    cd nginx
    
    ```

2. Get mysql ip to use as a host with:
    
    ```bash
    kubectl -n mysql get svc
    ```

3. Copy the CLUSTER-IP and replace it in MYSQL_HOST in configmap.yaml:
    ```
    MYSQL_HOST: <CLUSTER-IP>
    ```

4. Apply the Kubernetes manifests:

    ```bash
    cd mysql
    kubectl apply -f namespace.yaml
    kubectl -n nginx apply -f configmap.yaml
    kubectl -n nginx apply -f deployment.yaml
    kubectl -n nginx apply -f service.yaml
    
    ```

5. Verify the deployments:

    ```bash
    kubectl -n nginx get deployments
    kubectl -n nginx get pods
    kubectl -n nginx get svc
    kubectl -n nginx get configmap
    ```



## Usage

- **Accessing Nginx Server**: After deploying the Nginx server, use Minikube to obtain the service URL:

    ```bash
    minikube -n nginx service --url
    ```

    This command will provide you with the URL to access the Nginx server.

- **Interacting with MySQL Database**: Connect to the MySQL service endpoint using appropriate client tools (e.g., MySQL Workbench, command-line client) to interact with the database.

If you want to deploy additional applications, you can create new Kubernetes manifests or modify existing ones to include your application's deployment and service configurations.

