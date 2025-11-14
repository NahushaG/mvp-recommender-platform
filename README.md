# MVP Recommender Platform
A **live, deployable platform** for recommending the **Most Valuable Players (MVPs)** in Fantasy Premier League (FPL) using **AI-powered analysis**. The platform is containerized, server-ready, and uses **AWS ECS/Fargate, Terraform, Ansible (GitOps), and CI/CD** for automated deployment.

---

## **Project Overview**
MVP Recommender Platform fetches FPL data (players, fixtures, stats) and provides AI-powered recommendations for:

- Most valuable players (MVPs)  
- Budget-friendly squad suggestions  
- Custom analytics based on player performance  

The platform demonstrates **modern cloud deployment practices** and **infrastructure automation**.

---

## **Architecture**
[Frontend(React)]
    |
[S3 + CloudFront]
    |
[ALB/ API Gateway]
    |
[ECS Fargate(mvp-recommender Docker)]
    |
RDS Postgres/ Secrete Manager

## CI/CD FLow
[GitHub Repository] -> [GitHub Action CI] -> [Docker build & push] -> Ansible CD -> Terraform deploy on AWS

---

## **Tech Stack**
- **Frontend:** React.js
- **Backend:** JVM(Grails/Spring Boot)
- **Database:** PostgresSQL on AWS RDS
- **Containerizations:** Docker
- **Infrastructure as Code:** Terraform
- **Deployment Automation:** Ansible(GitOps)
- **CI/CD:** GitHub Actions
- **Hosting / Cloud:** AWS ECS Fargate, ALB, S3 + CloudFront
- **Secret Management:** AWS Secret Manager

## **Folder Structure**
``` text
mvp-recommender-platform/
├── backend/ # JVM backend source code
├── frontend/ # React frontend
├── Dockerfile # Containerize backend app
├── infra/
│ ├── terraform/ # AWS infrastructure provisioning
│ └── ansible/ # GitOps deployment scripts
├── .github/workflows/ # CI/CD GitHub Actions
└── README.md
```
## **Getting Started**
### **Prerequisites**
- AWS account with IAM credentials
- Docker & Docker Compose
- Terraform (v1.5+)
- Ansible (v2.10+)
- Node.js & npm
- GitHub account for CI/CD

### **Setup Steps**
1. **Clone the repository
```bash
git clone https://github.com/NahushaG/mvp-recommender-platform.git
cd mvp-recommender-platform
```
2. Create environment file
```bash
    cp .env_sample .env
```
Fill in your secrets:
* DB_USER, DB_PASSWORD, DB_NAME
* OPENAI_API_KEY
* AWS credentials if using Terraform locally

3. Build and test Docker image
```
docker build -t mvp-recommender .
docker run -p 8080:8080 mvp-recommender
```
4. Deploy Infrastructure(Terraform)
```
cd infra/terraform
terraform init
terraform plan
terraform apply
```
5. Deploy Application(Ansible/GitOps)
```
    cd infra/ansible
    ansible-playbook deploy/tasks/main.yml -i inventory/hosts.yml
```
6. Access the platform
* Frontend: S3 + CloudFront URL
* API: ALB or API Gateway URL

## CI-CD Worflow
- GitHub Actions CI:
    - Checkout code
    - Build & test backend(Gradle)
    - Build frontend assets
    - Build & push Docker image to ECR
- Ansible CD(GitOps)
    - Apply Terraform infrastructure
    - Update ECS Fargate service with new Docker image
    - Invalidate CloudFront cache

## Secrets Management
- Store sensitive info in AWS Secrets Manager or GitHub Secrets
    - DB_USER, DB_PASSWORD, DB_NAME
    - OPENAPI_API_KEY
    - AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY

## License
MIT License

## Author
Nahusha Ganiga



