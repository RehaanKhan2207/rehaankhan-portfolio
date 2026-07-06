# Task 4: Automated Deployment on Cloud VM with Nginx Reverse Proxy

## Project Objective
Closed the end-to-end DevOps lifecycle loop by transitioning from manual container deployment into a fully automated Continuous Deployment (CD) pipeline. GitHub Actions now securely orchestrates staging tasks directly on an live AWS EC2 instance using a production-grade Nginx Reverse Proxy routing infrastructure.

## Tools & Technologies Used
* **CI/CD Orchestration Engine:** GitHub Actions
* **Secure Remote Protocol:** SSH via OpenSSH (appleboy/ssh-action)
* **Web Server & Reverse Proxy:** Nginx (Engine X)
* **Container Environment:** Docker Engine

## Production Deployment Architecture
The updated pipeline abstracts network routing complexity and maintains the following security and traffic sequence:
1. **Trunk Push:** Code updates trigger an ephemeral pipeline on the `main` branch.
2. **Phase 1 (CI):** Builds and synchronizes the newest container configuration with Docker Hub.
3. **Phase 2 (CD):** GitHub Actions extracts deployment configurations from encrypted Repository Secrets (`VM_HOST`, `VM_USER`, `VM_SSH_KEY`) and establishes a secure runtime SSH session with the target AWS server.
4. **Server Orchestration Script:** * Fetches (`docker pull`) the newly refreshed container artifact down from the registry.
   * Terminates and cleans up any existing application states (`docker stop` & `docker rm`).
   * Spins up the application detached, binding it internally to loopback port `8080`.
5. **Reverse Proxy Architecture:** Nginx acts as an infrastructure shield on public Port `80`. It takes incoming internet requests and proxies them straight to the inner Docker application layer on Port `8080`.

## How to Verify Runtime Application
Open a web browser and navigate directly to the cloud instance's public IP mapping:
```text
[http://51.21.160.112](http://51.21.160.112)
