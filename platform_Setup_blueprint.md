# Platform implementation plan 
## Platform Deployment Selection 
Available options
* ECS/Fargate 
    - Package app as Docker container
    - Deploy to AWS ECS/Fargate
    - Scale automatically serverless container
* Elastic Bean
    - Simple JVM deployment, auto handles EC2 and load balancer
    - Easy for small projects
* AWS Lambda (Serverless)
    - Only feasible if the app is converted to serverless functions
    - Might be tricky for JVM apps with heavy dependency
* EKS/ Kubernetes
    - Containerized and deploy via kubernetes
    - Complex 
Since this project deals with CI/CD pipeline proficiency with mid complexity we hav gone with ECS/Fargate with Terraform + GitOps is ideal

## Dockerize the Applications
### Define Terraform Infrastructure
- ECS Cluster
- Fargate Service & Task Definition
- VPC / Subnet/ Security Groups
- Application Load Balancer
- RDS Database (Postgres)
- Secrets Manager (for OpenAI key, DB creds)
- CloudWatch logs
### Folder structure 
```text
infra/
└── terraform/
    ├── main.tf
    ├── variables.tf
    ├── outputs.tf
    └── provider.tf

## CI/CD Pipeline (GitHub Actions)
- CI Steps
    - Checkout
    - run
    - build
    - pist to registry (ECR)
- CD steps (GitOps via Ansible/Terraform)
    - Pull latest Terraform config
    - terraform plan & terraform apply
    - Update ECS service with new Docker image
    - Optional: healthcheck via ALB

## Secret & Environment Variables
    - Sensitive info related to project
    - Such as
        - DB_USER
        - DB_PASSWORD
        - DB_NAME
        - OPEN_API_KEY
    - ECS task defination pulls secrets automatically