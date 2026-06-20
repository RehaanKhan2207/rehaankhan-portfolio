# Task 2: Dockerized Portfolio Website Deployment

This project demonstrates the containerization and manual cloud deployment of a portfolio website using Docker and an Nginx web server running on an AWS EC2 virtual machine instance.

## 🛠️ Tech Stack & Architecture
- **Web Server:** Nginx (Alpine-based container image)
- **Container Runtime:** Docker Engine
- **Cloud Infrastructure:** AWS EC2 (Ubuntu 26.04 LTS, `t2.micro` Free Tier)

## 🚀 Step-by-Step Implementation Steps

### 1. Local Containerization & Testing
A custom configuration file (`Dockerfile`) was written to package the application:
```dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
EXPOSE 80
```

Tested locally by building the image and mapping the internal Nginx application port to host port 8080:

Bash
docker build -t portfolio-website .
docker run -d -p 8080:80 portfolio-website
2. Cloud Server Provisioning (AWS EC2)
Launched an Ubuntu 26.04 LTS instance (t2.micro).

Configured Inbound Security Group Rules to open Port 22 (SSH) for secure terminal administration and Port 80 (HTTP) to allow production web traffic from the open internet.

3. Server Configuration & Live Deployment
Connected to the virtual host machine via SSH using a secure keypair:

Bash
ssh -i portfolio-key.pem ubuntu@51.21.160.112
Installed the container architecture engine, updated system groups, cloned the GitHub code repository, and deployed the final operational layer:

Bash
# System Prep & Docker Installation
sudo apt update && sudo apt install docker.io -y
sudo systemctl start docker && sudo systemctl enable docker
sudo usermod -aG docker ubuntu

# Build and Deploy Application Container
git clone [https://github.com/RehaanKhan2207/rehaankhan-portfolio.git](https://github.com/RehaanKhan2207/rehaankhan-portfolio.git)
cd rehaankhan-portfolio
docker build -t portfolio-website .
docker run -d -p 80:80 portfolio-website
🌐 Live Access URL
The active container environment can be reached publicly via the internet at:
Link: http://51.21.160.112
