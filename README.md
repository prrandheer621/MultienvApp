# MultienvApp docker-skill-test
docker-skill-test 31 Jan


# Deploying and Running Flask App Using Docker and Docker Compose

This document provides step-by-step instructions for setting up, deploying, and troubleshooting a Flask backend application, and React frontend application using Docker and Docker Compose.

---

## Prerequisites
- Backend and frontend codes
- MongoDB connection strings
- Git and Docker installed.

---

## Step 1: Clone the Repository
1. Clone your repository:
   ```bash
   git clone https://github.com/prrandheer621/MultienvApp.git
   ```

2. Navigate to the project directory:
   ```bash
   cd MultienvApp
   ````
3. Navigate to backend/dev, backend/prod, frontend. Create Dockerfile in each of them, and write necessary codes.
---

## Step 2: Build and Run backend as well as frontend servers

### Build images for each.
```bash
docker build -t . bdev
docker build -t . bprod
docker build -t . frontend
```

### Run Each server
```bash
docker run -d -p 3001:3001 bdev:latest
docker run -d -p 3002:3002 bprod:latest
docker run -d -p 80:80 frontend:latest
```

### Verify Running Containers
```bash
docker ps
```

---

## Step 6: Troubleshooting

### 1. Cannot Access Application (Ports Blocked)
- Check the Docker file for exposed port, and run command if same port is mapped or not.
  
### 2. Check Docker Logs
If any container fails to start, inspect the logs:
```bash
docker logs <<container-name>>
```
## Step 3: Test servers
- Go to browser, and run localhost:3001, localhost:3002 and add some data.
- Go to localhost, and see if that data reflects there.
---

## Step 4: Automate with Docker Compose

### Edit `docker-compose.yml`
Ensure `docker-compose.yml` is correctly configured:
```yaml
version: '3'
services:
  bdev:
    container_name: bdev
    image: bdev
    build:
      context: ./backendDev
      dockerfile: Dockerfile
    ports:
      - "3001:3001"
  bprod:
    container_name: bprod
    image: bprod
    build:
      context: ./backendProd
      dockerfile: Dockerfile
    ports:
      - "3002:3002"
  frontend:
    container_name: frontend
    image: frontend
    build: 
      context: ./frontend
      dockerfile: Dockerfile
    ports:
      - "80:80"
```

### Run All Services with Docker Compose
```bash
docker-compose up --build
```

### Stop All Services
```bash
docker-compose down
```

---

## Step 9: Final Verification
1. Confirm all containers are running:
   ```bash
   docker ps
   ```

2. Test the services using their respective URLs or `curl`.

---

## Appendix: Useful Commands

### Remove All Containers
```bash
docker rm -f $(docker ps -aq)
```

### Remove All Images
```bash
docker rmi -f $(docker images -q)
```

### List Running Containers
```bash
docker ps
```

---
