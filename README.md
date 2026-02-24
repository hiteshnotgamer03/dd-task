CRUD DD Task — MEAN Stack DevOps Deployment

Overview
This project demonstrates the containerization, CI/CD automation, and cloud deployment of a full-stack MEAN (MongoDB, Express.js, Angular, Node.js) application.

The application is fully deployed on an Ubuntu Virtual Machine using Docker Compose with Nginx configured as a reverse proxy.

Architecture Overview

Frontend (Angular) → Nginx Reverse Proxy → Backend (Node.js + Express) → MongoDB Database

Infrastructure Components:
AWS EC2 Ubuntu Virtual Machine
Docker & Docker Compose
MongoDB (Docker Container)
GitHub Actions CI/CD Pipeline
Docker Hub Image Registry
Nginx Reverse Proxy

Repository Structure
.github/workflows/
    deploy.yml (CI/CD Pipeline)

backend/
    Dockerfile

frontend/
    Dockerfile

nginx/
    default.conf

docker-compose.yml

README.md

Repository Setup
Created a new GitHub repository.
Extracted provided MEAN stack project.
Added frontend and backend source code.
Created Dockerfiles for both services.
Configured GitHub Actions workflow.

Containerization
Dockerfiles were created separately for:
Backend (Node.js Express API)
Frontend (Angular Application)
Docker images are built automatically via CI/CD.
Docker Hub Images:
Backend:
cloudguy03/backend:v1
Frontend:
cloudguy03/frontend:v1

Cloud Infrastructure Setup
Platform Used:
AWS EC2 Ubuntu Server
Steps:
Created Ubuntu EC2 instance.
Enabled inbound rules:
Port 22 (SSH)
Port 80 (HTTP)
Port 5000 (Backend testing optional)
Installed Docker:
sudo apt update
sudo apt install docker.io -y
Installed Docker Compose.

Application Deployment (Docker Compose)
Deployment handled using:
docker-compose.yml
Services:
MongoDB Database
Backend API
Frontend Application
Nginx Reverse Proxy
Deployment Command:
docker-compose up -d
Check Containers:
docker ps

Database Setup
MongoDB deployed using official Docker Image.
mongo:latest
Persistent volume configured:
mongo-data:/data/db

Nginx Reverse Proxy Setup
Nginx container acts as reverse proxy.
Responsibilities:
Serves frontend application.
Routes API requests to backend service.
Application accessible via port 80.
Configuration File:
nginx/default.conf
Public Access:
http://<EC2-Public-IP>

CI/CD Pipeline
CI/CD implemented using GitHub Actions.
Workflow File:
.github/workflows/deploy.yml
Pipeline Workflow:
Trigger on push to main branch.
Checkout source code.
Login to Docker Hub using GitHub Secrets.
Build frontend Docker Image.
Build backend Docker Image.
Push images to Docker Hub.
GitHub Secrets Used:
DOCKER_USERNAME
DOCKER_PASSWORD

Automatic Deployment Strategy
Latest Docker images are pulled and containers restarted on the server using Docker Compose.
docker-compose pull
docker-compose up -d

Application URL: http://13.233.255.138

Verification Steps
SSH into Server:
ssh -i key.pem ubuntu@public-ip
Check Containers:
docker ps
Check Logs:
docker logs nginx

Author
Hitesh S
DevOps Internship Assignment Submission