🛒 Shopping Cart Application – DevOps CI/CD Pipeline

This project demonstrates how to set up an end-to-end CI/CD pipeline for a sample Java-based Shopping Cart web application.

⚠️ Note: The application source code is not authored by me. It was taken from open resources for learning purposes.
My contribution is focused on building the DevOps workflow – installing and configuring tools, setting up Jenkins pipelines, Dockerizing the application, integrating SonarQube for quality analysis, and deploying the containerized app.

📌 Project Workflow

Code → GitHub → Jenkins CI Pipeline → SonarQube → Maven Build → Docker Image Build & Push → Jenkins CD Pipeline → Deployment

⚙️ Tools & Technologies Used

AWS EC2 (t2.medium)

Jenkins – CI/CD automation

Maven – Build tool

Git – Source code management

SonarQube – Code quality & static analysis

Docker – Containerization & deployment

Docker Hub – Container registry

🚀 Setup Instructions
1️⃣ Launch EC2 Instance

Launch a t2.medium EC2 instance (Amazon Linux 2).

Connect via SSH.

2️⃣ Install Jenkins
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade -y
sudo dnf install java-17-amazon-corretto -y
sudo yum install jenkins -y
sudo systemctl daemon-reload
sudo systemctl enable jenkins
sudo systemctl start jenkins


Access Jenkins at: http://<EC2-Public-IP>:8080

3️⃣ Install Docker
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker

4️⃣ Install Git
sudo yum install git -y

5️⃣ Run SonarQube in Docker
docker run -d -p 9000:9000 sonarqube:lts-community


Open in browser: http://<EC2-Public-IP>:9000

Default credentials:

username: admin

password: admin (you’ll be prompted to update)

Generate a SonarQube token from:
Administration → Security → Users → Update Tokens → Generate Token

Use this token in Jenkins CI pipeline configuration.

6️⃣ Configure Jenkins Plugins

Install the following plugins:

OpenJDK / Eclipse Temurin Installer

SonarQube Scanner for Jenkins

Docker Pipeline

Docker Build Step

CloudBees Docker Build and Publish

7️⃣ Configure Jenkins Global Tools

JDK

Maven

SonarQube Scanner

Docker

8️⃣ Give Jenkins Access to Docker

By default, Jenkins cannot access the Docker daemon. Add Jenkins user to the Docker group:

sudo usermod -aG docker jenkins
sudo systemctl restart jenkins


Verify:

groups jenkins


→ should list docker.

9️⃣ Common Fix

If container already exists:

docker rm -f shopping-cart

🌍 Application Access

Once deployed, the shopping cart application is available at:

URL: http://<EC2-Public-IP>:8070/home

Admin Login

Username: admin

Password: admin

User Login

Username: user

Password: password

📖 Key Learnings

Setting up Jenkins and integrating with GitHub

Using SonarQube for code quality analysis

Dockerizing applications and pushing to Docker Hub

Managing Jenkins-to-Docker permissions

Deploying and accessing a Java web application in containers
