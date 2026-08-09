---
title: "Continuous Integration & Continuous Deployment"
date: 2026-08-07
weight: 5
chapter: false
pre: " <b> 5.3.5. </b> "
---

## Objective

Set up a **Continuous Integration & Continuous Deployment (CI/CD)** pipeline using **GitHub Actions** and **Amazon Elastic Container Registry (Amazon ECR)** to automate the process of building, storing, and deploying the **AI Learning Assistant Platform**.

The CI/CD pipeline allows the application to be automatically updated whenever new changes are pushed to the `main` branch of the GitHub Repository.

---

## Implementation

### Create an Amazon ECR Repository

**Amazon Elastic Container Registry (Amazon ECR)** is used to store and manage the Docker Images required by the AI Learning Assistant Platform.

Follow these steps:

1. Open the **AWS Management Console**.
2. Search for and open **Amazon Elastic Container Registry (ECR)**.
3. Select **Repositories**.
4. Click **Create repository**.
5. Set the repository name to: **ai-learning-assistant**
6. Select **Private** as the repository visibility.
7. Click **Create repository**.

After the repository is created, Amazon ECR provides a repository URI that is used by GitHub Actions to push Docker Images.

> **Figure 5.3.9. Amazon ECR repository for the AI Learning Assistant Platform.**

> ![Figure 5.3.9](/images/5.3.9.png)

---

### Configure GitHub Secrets

GitHub Actions requires credentials and deployment information to access AWS resources and the EC2 server.

To protect sensitive information, these values are stored using **GitHub Secrets** instead of being written directly into the workflow file.

Follow these steps:

1. Open the **GitHub Repository** of the project.
2. Select **Settings**.
3. Select **Secrets and variables**.
4. Select **Actions**.
5. Click **New repository secret**.

Configure the required secrets as follows:

| Secret | Purpose |
|--------|---------|
| **AWS_ACCESS_KEY_ID** | AWS access key used by GitHub Actions |
| **AWS_SECRET_ACCESS_KEY** | AWS secret access key used by GitHub Actions |
| **EC2_HOST** | Elastic IP address of the EC2 Instance |
| **EC2_USERNAME** | Username used to connect to the EC2 Instance |
| **EC2_SSH_KEY** | Private SSH key used by GitHub Actions to access EC2 |

The AWS credentials are obtained from the IAM configuration prepared in the previous steps.

For the EC2 deployment, the **EC2_HOST** value is the Elastic IP address of the server, while **EC2_UUSERNAME** is:

```text
ubuntu
```

The **EC2_SSH_KEY** contains the private SSH key required for GitHub Actions to establish an SSH connection to the EC2 Instance.

> **Security Note:** Never commit AWS credentials, private SSH keys, API Keys, passwords, or other sensitive information directly into the GitHub Repository.

> **Figure 5.3.10. GitHub Repository Secrets configured for the CI/CD pipeline.**

> ![Figure 5.3.10](/images/5.3.10.png)

---

### Configure GitHub Actions Workflow

After configuring the required GitHub Secrets, create the GitHub Actions workflow file:

```text
.github/workflows/deploy-aws.yml
```

The workflow is responsible for automatically building the Docker Image, pushing the Image to Amazon ECR, and deploying the latest version to Amazon EC2.

A simplified workflow process is shown below:

```text
Git Push
   |
   v
GitHub Actions
   |
   v
Build Docker Image
   |
   v
Amazon ECR
   |
   v
Deploy to Amazon EC2
   |
   v
Updated Application
```

The workflow is triggered whenever new code is pushed to the `main` branch.

Example workflow structure:

```yaml
name: Deploy AI Learning Assistant

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source code
        uses: actions/checkout@v4

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Login to Amazon ECR
        uses: aws-actions/amazon-ecr-login@v2

      - name: Build Docker Image
        run: |
          docker build -t ai-learning-assistant .

      - name: Tag Docker Image
        run: |
          docker tag ai-learning-assistant:latest \
            <ECR_REPOSITORY_URI>:latest

      - name: Push Docker Image to Amazon ECR
        run: |
          docker push <ECR_REPOSITORY_URI>:latest

      - name: Deploy to Amazon EC2
        run: |
          ssh -i "${{ secrets.EC2_SSH_KEY }}" \
            -o StrictHostKeyChecking=no \
            ${{ secrets.EC2_USERNAME }}@${{ secrets.EC2_HOST }} \
            "cd ~/AI-Learning-Assistant && git pull && docker compose up -d"
```

> **Note:** Replace `<ECR_REPOSITORY_URI>` with the actual URI of the Amazon ECR repository created in the previous step.

---

### Run the CI/CD Workflow

After the workflow file has been added to the repository, commit and push the changes to the `main` branch.

For example:

```bash
git add .
git commit -m "Configure AWS CI/CD pipeline"
git push origin main
```

After the push is completed, GitHub Actions automatically detects the new commit and starts the workflow.

The workflow performs the following steps:

1. Checkout the latest source code from GitHub.
2. Configure AWS credentials.
3. Authenticate with Amazon ECR.
4. Build the Docker Image.
5. Tag the Docker Image.
6. Push the Docker Image to Amazon ECR.
7. Connect to the Amazon EC2 Instance.
8. Deploy the latest application version.

The workflow status can be viewed by opening:

**GitHub Repository → Actions**

If all steps are completed successfully, GitHub Actions displays a green **Success** status.

> **Figure 5.3.11. GitHub Actions workflow completed successfully.**

> ![Figure 5.3.11](/images/5.3.11.png)

---

## Result

After completing this step, the **Continuous Integration & Continuous Deployment (CI/CD)** pipeline has been configured using **GitHub Actions** and **Amazon ECR**.

Whenever new code is pushed to the `main` branch, GitHub Actions automatically builds the Docker Image, pushes the Image to Amazon ECR, and deploys the updated application to Amazon EC2.

This automated workflow reduces manual deployment steps and provides a more consistent deployment process for the **AI Learning Assistant Platform**.

The CI/CD pipeline is now ready for testing and verification in the following sections.