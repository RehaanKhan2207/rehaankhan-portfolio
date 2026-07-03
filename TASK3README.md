# Task 3: Automated CI/CD Pipeline with GitHub Actions & Docker Hub

## Project Objective
Transitioned the manual container build and deployment process from Task 2 into a fully automated Continuous Integration (CI) delivery workflow using GitHub Actions. Every code modification pushed to the repository automatically triggers an isolated pipeline to test, build, and publish the verified environment.

## Tools & Technologies Used
* **Version Control:** Git & GitHub
* **CI Engine:** GitHub Actions (Ubuntu-latest runner)
* **Container Runtime:** Docker Engine
* **Centralized Registry:** Docker Hub
* **Configuration Language:** YAML

## CI/CD Pipeline Architecture
The workflow handles secure credentials management and builds infrastructure using the following sequence:
1. **Trigger:** Detects a `git push` event targeting the `main` branch.
2. **Environment Provisioning:** Spins up an isolated, ephemeral `ubuntu-latest` virtual runner.
3. **Checkout:** Clones the code securely using `actions/checkout@v3`.
4. **Authentication:** Establishes an encrypted session with Docker Hub using repository secrets (`DOCKER_USERNAME`, `DOCKER_PASSWORD`).
5. **Image Assembly:** Compiles the localized environment using the root `Dockerfile`.
6. **Central Shipment:** Tags and pushes the standardized compilation out to the public registry.

## How to Verify Deployment
Pull and execute the automated artifact directly from any network host using:
```bash
docker pull rehaankhan/portfolio-website:latest
docker run -d -p 8081:80 rehaankhan/portfolio-website:latest
Save and push it to GitHub:
```bash
git add TASK3README.md
git commit -m "docs: add comprehensive Task 3 documentation"
git push origin main
