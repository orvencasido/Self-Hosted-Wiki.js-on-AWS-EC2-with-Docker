# 🔐 Secure Ubuntu Server with UFW and Fail2Ban (SSH Hardening on AWS EC2)

This project demonstrates how to deploy Wiki.js — a powerful, modern, and open-source wiki engine — using Docker and Docker Compose with a PostgreSQL database.

---

## 🛠 Tools & Technologies

- Ubuntu (Linux)
- Docker
- Docker Compose
- PostgreSQL
- Wiki.js (Requarks Wiki)

---

## 🚀 Project Overview

- Installing Docker and Docker Compose on a Linux server
- Running a PostgreSQL container for the backend
- Deploying Wiki.js in a Docker container
- Accessing the Wiki.js web UI via your browser

---

## 📋 Step-by-Step Guide

### ✅ 1. Install Docker and Docker Compose
```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo systemctl start docker
sudo systemctl enable docker
```

### ✅ 2. Create a Project Directory
```
mkdir wikijs-docker
cd wikijs-docker
```

### ✅ 3. Create docker-compose.yml
```
nano docker-compose.yml
```

```
version: '3'

services:
  db:
    image: postgres:13
    restart: always
    environment:
      POSTGRES_DB: wikijs
      POSTGRES_USER: wikijs
      POSTGRES_PASSWORD: wikijsrocks
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: requarks/wiki:2
    restart: always
    depends_on:
      - db
    ports:
      - "3000:3000"
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wikijs

volumes:
  db-data:
```

### ✅ 4. Launch the Containers
```
docker-compose up -d
```

### ✅ 5. Access Wiki.js in the browser
```
http://your-server-ip:3000
```

### ✅ 6. Wiki.js Initial Setup
- Follow the web-based setup wizard
- Create an admin account
- Set a site name


## 📎 Commands Reference
- `docker-compose up -d` – Start containers in detached mode
- `docker ps` – View running containers
- `docker-compose logs -f` – View live logs
- `docker-compose down` – Stop and remove containers
- `docker volume ls` – List Docker volumes

## 💡 Real-World Use Cases
- Host internal team documentation
- Run a self-hosted knowledge base
- Use Wiki.js as a modern alternative to tools like Confluence or MediaWiki

## 📚 Learning Outcomes
- Set up Dockerized applications
- Deploy and configure PostgreSQL with Docker
- Use Docker Compose for multi-container setups
- Manage persistent volumes and environment variables

## 🧑‍💻 Author
Orven Casido – techwithorven.xyz
