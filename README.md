# AI-Automation-CI-CD
A repository showcasing AI automation, CI/CD, and deployment practices.
## Introduction

This repository highlights the use of AI automation and CI/CD practices in software development and deployment. It includes examples and demonstrations of tools and techniques used to automate workflows, ensure continuous integration, and deploy applications efficiently.

## Skills & Certifications
- Proficient in Azure DevOps, GitHub Actions, and Jenkins for CI/CD pipelines.
- Experienced with Terraform for infrastructure as code and AWS SageMaker for AI deployment.
- Certified in Stanford Machine Learning, Google Cloud Generative AI, and Duke University LLMOps.

## Code Examples

### GitHub Actions CI/CD Pipeline Example
```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.8'
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Run tests
      run: |
        pytest

  deploy:
    needs: build
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Deploy to AWS
      run: |
        # Add deployment commands here
```
This example demonstrates a basic CI/CD pipeline using GitHub Actions, including build, test, and deployment stages.

### Jenkins Pipeline Example
```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo Building...'
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'echo Testing...'
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'echo Deploying...'
                // Add deployment commands here
            }
        }
    }
}
```
This example demonstrates a Jenkins pipeline with build, test, and deploy stages, showcasing automation using Jenkins.

### Terraform Infrastructure Deployment Example
```hcl
provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "web_server" {
  ami           = "ami-0c94855ba95c71c99"
  instance_type = "t2.micro"

  tags = {
    Name = "WebServer"
  }
}
```
This example demonstrates a simple Terraform configuration for deploying an AWS EC2 instance, showcasing infrastructure as code.


### Dockerfile Example
```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```
This Dockerfile sets up a Python environment, installs dependencies, and runs a simple application.

### Kubernetes Deployment Example
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-server-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-server
  template:
    metadata:
      labels:
        app: web-server
    spec:
      containers:
      - name: web-server
        image: nginx:latest
        ports:
        - containerPort: 80
```
This example demonstrates a Kubernetes deployment with three replicas of an Nginx web server.

### Azure DevOps YAML Pipeline Example
```yaml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: UsePythonVersion@0
  inputs:
    versionSpec: '3.8'

- script: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt
  displayName: 'Install dependencies'

- script: |
    pytest
  displayName: 'Run tests'

- task: AzureCLI@2
  inputs:
    azureSubscription: 'Your-Azure-Subscription'
    scriptType: 'bash'
    scriptLocation: 'inlineScript'
    inlineScript: |
      # Add deployment script here
```
This example demonstrates a basic Azure DevOps YAML pipeline with steps for setting up Python, installing dependencies, running tests, and deploying using the Azure CLI.

### AWS SageMaker Deployment Example
```python
import boto3
from sagemaker import get_execution_role
from sagemaker.sklearn.estimator import SKLearn

role = get_execution_role()

estimator = SKLearn(entry_point='train.py',
                    role=role,
                    instance_type='ml.m5.large',
                    framework_version='0.23-1',
                    py_version='py3')

estimator.fit({'train': 's3://your-bucket/train-data'})

predictor = estimator.deploy(initial_instance_count=1, instance_type='ml.m5.large')
```
This example demonstrates deploying a machine learning model using AWS SageMaker.

### Google Vertex AI Deployment Example
```python
from google.cloud import aiplatform

project_id = "your-project-id"
model_display_name = "your-model-display-name"
endpoint_display_name = "your-endpoint-display-name"

model = aiplatform.Model.upload(
    display_name=model_display_name,
    artifact_uri="gs://your-bucket/model",
    serving_container_image_uri="us-docker.pkg.dev/vertex-ai/prediction/sklearn-cpu.0-24:latest",
)

endpoint = model.deploy(
    machine_type="n1-standard-4",
    endpoint_display_name=endpoint_display_name,
)
```
This example demonstrates deploying a machine learning model using Google Vertex AI.
