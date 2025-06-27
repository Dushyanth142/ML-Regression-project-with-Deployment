# End-to-End ML Regression Project with Automated AWS Deployment

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/downloads/)
[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)]
[![CI/CD](https://github.com/Dushyanth142/ML-Regression-project-with-Deployment/actions/badge.svg)](https://github.com/Dushyanth142/ML-Regression-project-with-Deployment/actions)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://www.docker.com/)
[![AWS](https://img.shields.io/badge/AWS-Deployed-orange.svg)](https://aws.amazon.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains an end-to-end machine learning project that predicts student performance based on various attributes. The project's primary focus on demonstrating a complete, automated CI/CD pipeline for building, testing, and deploying a web application to the AWS cloud.

## 🏛️ Architecture & CI/CD Workflow

This project leverages **GitHub Actions** for automation. On every push to the `main` branch, the following CI/CD pipeline is triggered:

1.  **GitHub Push (Trigger):** The workflow starts when new code is pushed to the `main` branch.
2.  **Docker Build:** GitHub Actions builds a Docker image of the Flask application using the `Dockerfile`.
3.  **Push to AWS ECR:** The newly built Docker image is tagged and pushed to a private Amazon Elastic Container Registry (ECR).
4.  **Deploy to AWS EC2:** The workflow securely connects to a pre-configured AWS EC2 instance, pulls the latest Docker image from ECR, and runs it as a container, making the updated application live.

## ✨ Features

-   **End-to-End Regression Model:** A complete pipeline for data preprocessing, training, and inference.
-   **Web Application:** A user-friendly interface built with Flask to interact with the model.
-   **Automated CI/CD:** A robust GitHub Actions workflow automates the entire deployment process.
-   **Cloud Deployment:** The application is fully deployed and operational on the AWS cloud (ECR for registry, EC2 for hosting).
-   **Containerized & Scalable:** Using Docker ensures consistency across environments and allows for easy scaling.
-   **Structured Python Package:** The source code is organized as an installable Python package, following best practices in software engineering.

## 🛠️ Tech Stack

-   **Machine Learning:** Python, Scikit-learn, Pandas, NumPy
-   **Web Framework:** Flask
-   **CI/CD:** GitHub Actions
-   **Cloud & Deployment:** AWS (EC2, ECR, IAM), Docker
-   **Project Structure:** Installable Python Package (`setup.py`)

## 📁 Project Structure

```
ML-Regression-project-with-Deployment/
│
├── .github/workflows/         # GitHub Actions CI/CD workflow files
│   └── main.yml
│
├── artifacts/                 # Stores trained model (model.pkl) and preprocessor
│
├── notebook/
│   └── EDA.ipynb              # Jupyter Notebook for EDA and model experimentation
│
├── src/                       # Source code, structured as a Python package
│   ├── components/            # Data ingestion, transformation, model training modules
│   ├── pipeline/              # Training and prediction pipelines
│   └── ...
│
├── templates/                 # HTML templates for the Flask application
│   └── index.html
│
├── .gitignore
├── app.py                     # Main Flask application entry point
├── Dockerfile                 # Docker instructions for containerization
├── requirements.txt           # Project dependencies
├── setup.py                   # Makes the `src` code an installable package
└── README.md                  # You are here!

```

## ⚙️ How to Run Locally

To run the application on your local machine, follow these steps:

### 1. Clone the Repository
```bash
git clone [https://github.com/Dushyanth142/ML-Regression-project-with-Deployment.git](https://github.com/Dushyanth142/ML-Regression-project-with-Deployment.git)
cd ML-Regression-project-with-Deployment
```

### 2. Create a Virtual Environment and Install Dependencies
```bash
# Create a virtual environment
python -m venv venv

# Activate it (Windows)
venv\Scripts\activate

# Activate it (macOS/Linux)
source venv/bin/activate

# Install the dependencies
pip install -r requirements.txt
```

### 3. Run the Flask Application
```bash
python app.py
```
Navigate to `http://127.0.0.1:5000` in your browser to see the app running.


## ☁️ Replicating the AWS Deployment

This section outlines the steps to set up the complete CI/CD pipeline.

### 1. Prerequisites
-   An **AWS Account** with administrative access.
-   A **GitHub Repository** with your project code.

### 2. Set Up AWS Resources
-   **IAM User:** Create an IAM user with programmatic access and policies for ECR and EC2 (`AmazonEC2ContainerRegistryFullAccess`, `AmazonEC2FullAccess`). Save the `Access Key ID` and `Secret Access Key`.
-   **ECR Repository:** Create a new private ECR repository to store your Docker images. Note the repository URI.
-   **EC2 Instance:** Launch a new EC2 instance (e.g., `t2.micro` with Ubuntu). Ensure the security group allows inbound traffic on the port your application runs on (e.g., port 5000).

### 3. Configure the EC2 Instance
Connect to your EC2 instance and install Docker.
```bash
# Update package lists
sudo apt-get update -y
sudo apt-get upgrade -y

# Install Docker
curl -fsSL [https://get.docker.com](https://get.docker.com) -o get-docker.sh
sudo sh get-docker.sh

# Add the current user to the docker group to run docker commands without sudo
sudo usermod -aG docker $USER
newgrp docker
```
### 4. Configure GitHub Actions
-   **Self-Hosted Runner (Optional but Recommended):** For better security and control, configure your EC2 instance as a GitHub self-hosted runner. Follow the instructions in your repository's settings (`Settings > Actions > Runners > New self-hosted runner`).
-   **GitHub Secrets:** In your GitHub repository settings (`Settings > Secrets and variables > Actions`), add the following secrets:
    -   `AWS_ACCESS_KEY_ID`: Your IAM user's access key.
    -   `AWS_SECRET_ACCESS_KEY`: Your IAM user's secret access key.
    -   `AWS_REGION`: The AWS region of your resources (e.g., `us-east-1`).
    -   `AWS_ECR_LOGIN_URI`: The URI of your ECR repository (e.g., `566373416292.dkr.ecr.us-east-1.amazonaws.com`).
    -   `ECR_REPOSITORY_NAME`: The name of your ECR repository.

### 5. Trigger the Deployment
Commit and push a change to your `main` branch. This will trigger the GitHub Actions workflow, which will automatically build and deploy your application to the EC2 instance.

## 📊 Dataset

This project uses a student performance dataset to predict final test scores. The features include:
-   **hours_studied:** The total number of hours the student spent studying.
-   **previous_scores:** The student's scores in previous exams.
-   **extracurricular_activities:** (Binary) Whether the student participates in extracurriculars.
-   **sleep_hours:** The average hours of sleep the student gets.
-   **sample_papers_practiced:** The number of practice papers completed.
-   **target (score):** The final test score, which the model aims to predict.
---
