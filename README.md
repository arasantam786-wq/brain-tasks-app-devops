DevOps Practice Project – Dist Directory

This repository contains the production-ready build files (dist folder) for DevOps practice and deployment exercises.

It is intentionally structured to help learners focus on CI/CD pipelines, hosting, containerization, and infrastructure setup rather than application development.

📁 What This Repository Contains

dist/ – Compiled and production-ready static files

HTML

CSS

JavaScript

Assets (images, fonts, etc.)

These files are ready to deploy to:

Web servers (Nginx / Apache)

Cloud platforms (AWS S3, Azure Blob, GCP Storage)

Containerized environments (Docker + Nginx)

Kubernetes clusters

CI/CD pipeline demonstrations

🎯 Purpose of This Repository

This repository is designed for:

DevOps beginners

CI/CD practice

Deployment pipeline testing

Docker & Kubernetes deployment exercises

Web server configuration practice

Reverse proxy and load balancer setup

The goal is to simulate real-world deployment scenarios using already built application files.

❓ Why is there NO package.json?

You may notice that this repository does not include:

package.json

node_modules

Source code (src/)

Build tools configuration

✅ Reason:

This repository only contains the final production build output (dist), not the development source code.

In a typical project:

Developers write source code.

The project is built using tools like:

Node.js

Webpack

Vite

React (or other frameworks)

A dist/ folder is generated.

Only the production build is deployed to servers.

This repository represents step 4 only.

Since this is already the compiled output:

# Brain Tasks App — AWS Deployment

## Overview
Brain Tasks application deployed on Amazon EKS using an automated AWS pipeline.

## Tools Used
- GitHub: source code
- Docker: application container
- AWS CodeBuild: build the Docker image
- Amazon ECR: store Docker images
- Amazon EKS: run the application
- AWS CodePipeline: automate build and deployment
- Amazon CloudWatch: monitoring and logs

## Pipeline Flow
GitHub → CodeBuild → ECR → EKS

1. Changes are pushed to the main branch.
2. CodePipeline retrieves the source code.
3. CodeBuild builds and pushes the Docker image to ECR.
4. The Deploy stage applies the Kubernetes deployment to EKS.

## Setup Instructions
1. Clone this repository.
2. Create the ECR repository: brain-tasks-app.
3. Create the EKS cluster: brain-tasks-eks, with worker nodes.
4. Configure IAM permissions for building images and deploying to EKS.
5. Create the CodeBuild project: brain-tasks-codebuild.
6. Set the buildspec path to dist/buildspec.yml and enable privileged mode for Docker.
7. Create the pipeline: brain-tasks-pipeline, using the main branch.
8. Configure the Deploy action:
   - Input artifact: BuildArtifact
   - Manifest file: dist/deployment.yaml
   - Cluster: brain-tasks-eks
9. Give the pipeline role EKS access to the default namespace.
10. Apply the service manifest:
    kubectl apply -f dist/service.yaml
11. Run the pipeline and verify the deployment.

## Verification Commands
```bash
kubectl get nodes
kubectl get pods
kubectl rollout status deployment/brain-tasks-app
kubectl get service brain-tasks-service
```

## Application URL
http://k8s-default-braintas-0d64f366e0-dc20b881dcd4b1ba.elb.ap-south-1.amazonaws.com

## Load Balancer ARN
arn:aws:elasticloadbalancing:ap-south-1:060651979375:loadbalancer/net/k8s-default-braintas-0d64f366e0/dc20b881dcd4b1ba

## Monitoring
Build log group:
/aws/codebuild/brain-tasks-codebuild

Deployment log group:
/aws/codepipeline/brain-tasks-pipeline

Application log group:
ADD_THE_LOG_GROUP_AFTER_APPLICATION_LOGGING_IS_CONFIGURED

## Screenshots
### Successful Pipeline
![Pipeline](screenshots/pipeline-success.png)

### Running Kubernetes Pods
![Pods](screenshots/running-pods.png)

### Working Application
![Application](screenshots/application.png)

### CloudWatch Build Logs
![Build logs](screenshots/cloudwatch-build.png)

### CloudWatch Deployment Logs
![Deployment logs](screenshots/cloudwatch-deploy.png)

### CloudWatch Application Logs
![Application logs](screenshots/cloudwatch-application.png)

No dependencies are required

No build process is required

No package.json is needed
