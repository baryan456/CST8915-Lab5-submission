# CST8915 — Lab 5 | Containerizing the Algonquin Pet Store

For this lab, I worked with the Algonquin Pet Store application, focusing on containerizing its services and running them together using Docker Compose.

I selected the Python implementation of the Product Service, alongside the Node.js Order Service and Vue.js Store Front. The frontend is built using Node.js and served through Nginx, while RabbitMQ handles asynchronous order messaging.

## Source Code & Published Images

I used the provided service repositories, added Dockerfiles, built the application images, and published them to my public Docker Hub repositories.

| Component | Source Code | Docker Image |
|---|---|---|
| Orders (Node.js) | [Order Service GitHub](ADD_YOUR_ORDER_FORK_URL) | [Docker Hub](https://hub.docker.com/r/baryan456/order-service) |
| Products (Python) | [Product Service GitHub](ADD_YOUR_PYTHON_PRODUCT_FORK_URL) | [Docker Hub](https://hub.docker.com/r/baryan456/product-service) |
| Frontend (Vue + Nginx) | [Store Front GitHub](ADD_YOUR_STOREFRONT_FORK_URL) | [Docker Hub](https://hub.docker.com/r/baryan456/store-front) |

For RabbitMQ, I used the official `rabbitmq:4.3.6-management` image.

## Running the Application

The final Docker Compose configuration references the published Docker Hub images instead of building the application locally.

First, copy `.env.example` to `.env` and configure the RabbitMQ credentials.

Pull the images:

```powershell
docker compose pull
```

Start all services:

```powershell
docker compose up -d --wait
```

Check the running containers:

```powershell
docker compose ps
```

Once the containers are running, the application is available at:

- **Store Front:** http://localhost:8080
- **Product Service:** http://localhost:3030/products
- **Order Service:** http://localhost:3000
- **RabbitMQ Management:** http://localhost:15672

## Store Front API Configuration

The Store Front image was built with the following API URLs embedded in its frontend configuration:

| Service | Embedded API URL |
|---|---|
| Order Service | `http://localhost:3000` |
| Product Service | `http://localhost:3030` |

**Embedded API host:** `localhost`

The frontend uses these URLs to communicate with the backend services through the browser on the local machine.

## Verification

I built the three application images locally and tested the services before running the complete application using Docker Compose.

After publishing the images to Docker Hub, I replaced the local build configuration with an image-only Docker Compose configuration.

I then pulled the published images and successfully started all four containers: Order Service, Product Service, Store Front, and RabbitMQ.

I also verified that the RabbitMQ `order_queue` was durable and received order messages.

## Challenges and Lessons Learned

This lab helped me understand the complete Docker workflow, from writing Dockerfiles and building images to tagging and publishing images to Docker Hub.

One important part of the lab was switching from locally built images to images pulled directly from Docker Hub. I also gained practical experience using Docker Compose to manage multiple services and RabbitMQ to handle asynchronous messaging.

Working with the multi-stage Docker build for the Vue frontend helped me understand how to separate the frontend build environment from the Nginx environment used to serve the application.

Overall, this lab improved my understanding of containerization, image distribution, and running multi-container applications.

## Demo Video

[**YouTube Demo**](https://youtu.be/AnP_0lfIavk)

The demonstration covers the running application, product loading, order placement, RabbitMQ queue verification, running containers, and public Docker Hub repositories.