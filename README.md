# Automated Static Website Deployment using Terraform & GitHub Actions
Live Demo URL: http://alpha-project-static-site-2310.s3-website.eu-central-1.amazonaws.com/

## Objective
The objective of this project was to design and implement a simple yet complete DevOps CI/CD pipeline for deploying a static website to Amazon Web Services (AWS S3) using Infrastructure as Code (Terraform) and GitHub Actions.
The main goal was to understand how automated deployment works in practice - from validating code to provisioning cloud resources and delivering changes automatically after each commit.

## Automation Workflow
- **Infrastructure as Code**: The entire cloud infrastructure (S3 buckets for website hosting and remote state, public access policies) is defined declaratively using Terraform. The Terraform state is securely stored in a private S3 bucket to enable collaboration and automation.
- **CI/CD Workflows**: The project uses two separate GitHub Actions workflows for a secure and robust pipeline:
  - A **Validation workflow** (`validate.yml`) runs on every Pull Request. It checks HTML syntax and validates the Terraform code for correctness and style, acting as a quality gate.
  - A **Deployment workflow** (`deploy.yml`) triggers automatically on every push to the main branch, but only after the validation workflow has successfully completed.
- **Deployment Process**: The deployment job applies the Terraform configuration to ensure the infrastructure is up-to-date and then synchronizes the contents of the `/website` folder with the public S3 bucket.

## Tools Used
- **Terraform** – Infrastructure as Code (IaC) tool for managing AWS resources declaratively.
- **AWS S3** – Cloud storage used for static website hosting and remote state storage.
- **AWS IAM** – Identity and Access Management for secure integration between GitHub Actions and AWS.
- **GitHub Actions** – CI/CD automation platform for running validation and deployment pipelines.
- **HTML tidy** – Command-line validator for syntax checking of HTML files.
- **GitHub Secrets** – Securely stores AWS credentials and environment variables.
- **Linux (Ubuntu-latest runner)** – Execution environment for pipelines.  

Future Improvements
- Add CloudFront as a CDN for HTTPS, improved performance, and caching.
- Introduce GitHub Environments for separate dev/staging/prod pipelines.
- Implement Terraform modules for a more modular and reusable infrastructure design.
- Add security scanning (e.g., Terrascan) step in CI for IaC best practices validation.
- Set up DynamoDB for Terraform state locking to prevent conflicts in a team environment.
