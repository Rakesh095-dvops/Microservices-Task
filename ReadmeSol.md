# Introduction 

This ```md``` file contains detailed steps how to build micro service using Docker (```Dockerfile``` and ```docker-compose.yml```) and tested using Docker Desktop locally.

## 1. Dockerfile Creation,Build and Test 
Create a Dockerfile for each service and test it individually.

### 1.1. User-service 
![alt text](Microservices/images/image.png)
![alt text](Microservices/images/image-1.png)

### 1.2. Product-service

![alt text](Microservices/images/0_docker_product_build.png)
![alt text](Microservices/images/0_docker_product_tst.png)

### 1.3. Order-service
![alt text](Microservices/images/1_docker_order_build.png)
![alt text](Microservices/images/1_docker_order_test.png)

### 1.4. Gateway-service
![alt text](Microservices/images/2_docker_gateway_build.png)
![alt text](Microservices/images/2_docker_gateway_test.png)

> ***Note*** - ```curl http://localhost:3003/api/users``` or any other gateway service result in error as each container is hosted on its own container network. 
>1. Create ```docker network create myapp-network``` and run each container again against that network to make gateway api works. 
>2. Sample example ```docker run -d --network myapp-network -p 3003:3003 --name gateway-service-container gateway-service```

## 2.  Docker Compose Creation,Build and Test 

### 2.1. docker-compose.yml 
Create a docker compose yml file and use below commands to build and test it 

```bash
# Build and start all services
docker-compose up -d

# Verify all containers are running
docker-compose ps

# View logs for all services
docker-compose logs -f

# Stop all services
docker-compose down
```

> ***Note*** - in case you are facing running any specific container use below-mentioned troubleshooting steps 
```bash
#Rebuild the Docker Images
#Run the following command to rebuild the Docker images:
docker-compose build user-service
# Debug the Build Context
docker build --no-cache -t user-service ./user-service
#Inspect the Container
docker-compose up -d user-service
docker exec -it user-service sh
ls /usr/src/app
#Clean Up Docker Cache
docker-compose down --rmi all --volumes --remove-orphans
docker-compose build --no-cache
docker-compose up
```
### 2.2. Successful build using docker-compose
![alt text](Microservices/images/3_docker_compose_build.png)
### 2.3. Verified all containers are running 
![alt text](Microservices/images/3_docker_compose_check_ps.png)
### 2.4. View logs for all services
![alt text](Microservices/images/3_docker_compose_logs.png)
### 2.5. Test each microservice using curl 
![alt text](Microservices/images/3_nodejs_apptest_usingcurl.png)
### 2.6. Terminate the docker compose
![alt text](Microservices/images/3_docker_compose_down.png)