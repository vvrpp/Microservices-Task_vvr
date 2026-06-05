# Submitted By: v venkata ramana

# Microservices Containerization Assignment

## Overview

This repository contains a containerized microservices application orchestrated using Docker and Docker Compose. The application comprises three backend services-**User Service**, **Product Service**-along with a centralized **Gateway Service** that serves as the single entry point for API consumption. All communication between the services is isolated within a dedicated, secure virtual bridge network.

## Setup and Deployment Instructions

### Prerequisites

Ensure your local host machine has the following tools installed:

- Linux Environment (Ubuntu/Debian)
- Modern Docker Engine (Docker Engine v20.10+)
- Docker Compose V2 Command Line Tool (docker compose)

### Deployment Steps

- Open your terminal and navigate to the project root directory:

cd ~/Downloads/anupamGithub/githublearning/

git clone https://github.com/vvrpp/Microservices-Task_vvr.git

cd C:\Users\vvrpa\OneDrive\Desktop\skilltest_1\Microservices-Task_vvr

- Build the decoupled resource layers and spin up the microservices network cluster simultaneously:

docker compose up -build

<img width="1071" height="207" alt="image" src="https://github.com/user-attachments/assets/486efed4-c536-46a4-88e4-df73b630933f" />

<img width="1834" height="537" alt="image" src="https://github.com/user-attachments/assets/96aeb77e-ceaa-4ed5-8961-cfbeb7e188a5" />

<img width="1834" height="537" alt="image" src="https://github.com/user-attachments/assets/c3d2d185-6044-4fbf-9eff-bec33475d22f" />


## Services and Endpoints Verification

Each isolated service exposes an active interface on the local interface (localhost). You can validate network responses using a terminal tool like curl or directly using a modern web browser.

### User Service

**Base URL:** <http://localhost:3000>

#### Testing Route

curl <http://localhost:3000/users>

**Browser Access Link:** <http://localhost:3000/users>

### Product Service

**Base URL:** <http://localhost:3001>

#### Testing Route

curl <http://localhost:3001/products>

**Browser Access Link:** <http://localhost:3001/products>

### Gateway Service (Unified Entrypoint)

**Base URL:** <http://localhost:3003/api>

#### Testing Downstream Proxy Routing Routes

**Proxied Users Payload**

curl <http://localhost:3003/api/users>

**Proxied Products Payload**

curl <http://localhost:3003/api/products>

**Proxied Orders Payload**

curl <http://localhost:3003/api/orders>

<img width="1317" height="107" alt="image" src="https://github.com/user-attachments/assets/86af9b28-c02a-42f3-8fa7-01096174e943" />

***Testing from within the container to another one***

from gateway service container to product and user service container
<img width="1832" height="481" alt="image" src="https://github.com/user-attachments/assets/8b34fe12-d9a3-49ff-b2dd-8a69cf172bf7" />

from user service container to product and gateway service container
<img width="1832" height="481" alt="image" src="https://github.com/user-attachments/assets/9c071862-23f0-444b-bb8a-3c5460ca371a" />

from product service container to user and gateway service container
<img width="1832" height="481" alt="image" src="https://github.com/user-attachments/assets/fa1ef65e-c764-4739-ba5c-218b59976c25" />


## Runtime Verification (Services Status)

When the ecosystem initializes successfully, the container management stack maps resources according to the blueprint, outputting the structure below:

\[+\] Running 7/7

✔ Network microservices-task-mohan_microservices-network Created 0.0s

✔ Container microservices-task-mohan-product-service-1 Started 0.1s

✔ Container microservices-task-mohan-user-service-1 Started 0.1s

✔ Container microservices-task-mohan-order-service-1 Started 0.1s

✔ Container microservices-task-mohan-gateway-service-1 Started 0.0s

Attaching to gateway-service-1, order-service-1, product-service-1, user-service-1

user-service-1 | User service running on port 3000

product-service-1 | Product service running on port 3001

order-service-1 | Order service running on port 3002

gateway-service-1 | Gateway service running on port 3003

Placing actual execution terminal screenshots or operational interface views under this section to visually prove local evaluation readiness.

<img width="1165" height="431" alt="image" src="https://github.com/user-attachments/assets/cc0d4125-4710-4c32-8707-e8ee5db33d27" />
<img width="999" height="131" alt="image" src="https://github.com/user-attachments/assets/841b7c85-40c5-4c76-9f83-d725e0b700e5" />

<img width="1327" height="171" alt="image" src="https://github.com/user-attachments/assets/e71766d9-c8a0-43c5-8367-d7e4545e6eb7" />

## DockerFile

	A. user-service
	FROM node:18-alpine
	WORKDIR /usr/src/app
	COPY package*.json ./
	RUN npm install
	COPY . .
	EXPOSE 3000
	CMD ["node", "app.js"]

	B. Product service
	FROM node:18-alpine
	WORKDIR /usr/src/app
	COPY package*.json ./
	RUN npm install
	COPY . .
	EXPOSE 3001
	CMD ["node", "app.js"]

	C. gateway-service
	FROM node:18-alpine
	WORKDIR /usr/src/app
	COPY package*.json ./
	RUN npm install
	COPY . .
	EXPOSE 3003
	CMD ["node", "app.js"]


## Basic Troubleshooting Tips

### 1\. Route Error Responses (Cannot GET /)

**Symptom:** Terminal or browser outputs a Cannot GET / string inside an HTML structure.

**Resolution:** This response validates that the container and port forwarding are operating correctly. The Express framework inside the application requires a specific path. Append the route context (e.g., /users, /products, /orders, or /api/users) to the end of your host link to view data arrays.

### 2\. Networking Host Conflicts (bind: address already in use)

**Symptom:** Containers stop unexpectedly or log a loopback proxy interface allocation error.

**Resolution:** A system loop or process on your local host system is already listening on ports 3000, 3001, 3002, or 3003. Stop the background host processes or update the host forwarding reference parameter on the left-hand side of the mapped elements inside the docker-compose.yml configuration.
