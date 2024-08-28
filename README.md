# Pipeline With Infracost

This project automates the deployment of AWS infrastructure using Terragrunt, integrated with GitHub Actions for continuous deployment. The infrastructure includes a Virtual Private Cloud (VPC), Security Groups (SG), and a Bastion EC2 instance. Infracost is used to estimate the cost of the infrastructure changes, and the results are posted as comments on pull requests.

## Table of Contents

- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [GitHub Actions Workflow](#github-actions-workflow)
- [Infracost Integration](#infracost-integration)
- [Contributing](#contributing)

## Introduction

"Pipeline With Infracost" automates the deployment of a secure AWS infrastructure using Terragrunt. It integrates seamlessly with GitHub Actions, enabling continuous integration and deployment (CI/CD) workflows. The infrastructure components include:

- **VPC (Virtual Private Cloud)**: Provides a logically isolated network for your resources.
- **Security Groups (SG)**: Acts as a virtual firewall to control inbound and outbound traffic for your instances.
- **Bastion EC2 Instance**: A secure server used to access your private instances in the VPC.

## Prerequisites

Before you begin, ensure you have the following:

- **AWS Account**: To deploy the infrastructure.
- **GitHub Account**: To use GitHub Actions for CI/CD.
- **Terraform**: Installed locally for testing.
- **Terragrunt**: Installed locally for managing Terraform configurations.
- **Infracost**: Installed for cost estimation (optional).

## Setup

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/pipeline_with_infracost.git
   cd pipeline_with_infracost

2. **Install Dependencies**:
Ensure you have Terraform and Terragrunt installed on your local machine.
Install Infracost if you plan to run cost estimates locally.

3. **Configure AWS Credentials:**:
Ensure your AWS credentials are set up correctly. You can use AWS CLI to configure them:
```bash
aws configure
```

4. **Set Up GitHub Secrets**:
Go to your repository settings on GitHub.
Navigate to Settings > Secrets and variables > Actions.
Add the following secrets:
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_SESSION_TOKEN (if applicable)
PAT_TOKEN/GITHUB_TOKEN (your GitHub Personal Access Token for posting comments)

## Usage
1. **Deploying the Infrastructure**
Local Deployment:
- To test the deployment locally, navigate to the dev environment directory and run:
```bash
terragrunt run-all apply
```

2. **Using GitHub Actions**:
- The GitHub Actions workflow automatically deploys the infrastructure when changes are pushed to the main branch.
- It also posts Infracost estimates as comments on pull requests.

**Reviewing Infracost Estimates**

- When you create or update a pull request, the GitHub Actions workflow will automatically run and post a comment with the Infracost estimate.
- The comment provides a detailed breakdown of the costs associated with the changes.

## Project Structure
```css
pipeline_with_infracost/
├── dev/
│   ├── terragrunt.hcl
│   ├── vpc/
│   │   └── terragrunt.hcl
│   ├── sg/
│   │   └── terragrunt.hcl
│   └── ec2/
│       └── terragrunt.hcl
├── modules/
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── sg/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── ec2/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
├── .github/
│   └── workflows/
│       └── cicd.yml
├── .gitignore
└── README.md
```

- dev/: Contains the terragrunt.hcl files for each component of the development environment (VPC, SG, EC2).
- modules/: Reusable Terraform modules for VPC, SG, and EC2.
- .github/workflows/: GitHub Actions workflow configuration.

## GitHub Actions Workflow 

The GitHub Actions workflow (.github/workflows/cicd.yml) automates the following tasks:

- Terraform Initialization: Initializes the Terraform environment.
- Terragrunt Formatting: Checks the formatting of terragrunt.hcl files.
- Infrastructure Deployment: Applies the Terraform configuration via Terragrunt.
- Infracost Integration: Calculates cost estimates and posts them as comments on pull requests.

## Infracost Integration

Infracost is integrated into the CI/CD pipeline to provide cost estimates for infrastructure changes. It helps in understanding the cost implications of your Terraform changes before they are applied.

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request with your changes. For major changes, please open an issue to discuss what you would like to change.