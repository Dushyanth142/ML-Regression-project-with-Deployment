
# 🧠 ML Regression Project with Automated AWS Deployment

A complete end-to-end machine learning regression project to predict student performance — featuring data preprocessing, model training, a web interface, and automated CI/CD deployment to AWS using Docker and GitHub Actions.

---

## 📚 Table of Contents

1. [🚀 Project Overview](#-project-overview)  
2. [🧰 Tech Stack](#-tech-stack)  
3. [📁 Folder Structure](#-folder-structure)  
4. [⚙️ Local Setup Instructions](#️-local-setup-instructions)  
5. [☁️ AWS CI/CD Deployment Guide](#️-aws-cicd-deployment-guide)  
6. [📊 Dataset Overview](#-dataset-overview)  
7. [📜 License](#-license)

---

## 🚀 Project Overview

This project demonstrates how to build and deploy a regression model with a full CI/CD pipeline using GitHub Actions, Docker, and AWS.

### Key Highlights:
- **ML Regression Pipeline**: From EDA to model training.
- **Web Interface**: Built using Flask.
- **Dockerized App**: Ensures reproducibility and scalability.
- **CI/CD Automation**: Seamless deployment pipeline using GitHub Actions.
- **Cloud Deployment**: Hosted using AWS EC2 and ECR.

---

## 🧰 Tech Stack

| Layer         | Technology                     |
|---------------|---------------------------------|
| ML & Data     | Python, Pandas, NumPy, Scikit-learn |
| Web Framework | Flask                          |
| DevOps        | Docker, GitHub Actions          |
| Cloud         | AWS EC2, AWS ECR, IAM           |

---

## 📁 Folder Structure

```
ML-Regression-project-with-Deployment/
│
├── .github/workflows/         # GitHub Actions CI/CD workflow
├── artifacts/                 # Trained model and preprocessor files
├── notebook/                  # Jupyter notebook for EDA
├── src/                       # Source code as Python package
│   ├── components/            # Data ingestion, transformation, etc.
│   ├── pipeline/              # Training & prediction pipeline
│   └── ...
├── templates/                 # HTML template for Flask UI
├── app.py                     # Entry point for Flask app
├── Dockerfile                 # For containerization
├── requirements.txt           # Python dependencies
├── setup.py                   # Installable Python module
└── README.md                  # Project documentation
```

---

## ⚙️ Local Setup Instructions

Follow these steps to run the application on your local system:

### 1. Clone the Repository

```bash
git clone https://github.com/Dushyanth142/ML-Regression-project-with-Deployment.git
cd ML-Regression-project-with-Deployment
```

### 2. Create Virtual Environment & Install Dependencies

```bash
# Create virtual environment
python -m venv venv

# Activate (Windows)
venv\Scripts\activate

# Activate (macOS/Linux)
source venv/bin/activate

# Install requirements
pip install -r requirements.txt
```

### 3. Run the Flask App

```bash
python app.py
```

Open your browser and navigate to [http://127.0.0.1:5000](http://127.0.0.1:5000)

---

## ☁️ AWS CI/CD Deployment Guide

### 1. Prerequisites
- AWS Account
- GitHub Repository
- IAM User with access to EC2 and ECR

### 2. AWS Setup

#### IAM
- Create IAM User
- Attach Policies:
  - `AmazonEC2FullAccess`
  - `AmazonEC2ContainerRegistryFullAccess`

#### ECR
- Create a private ECR repository
- Note down the repository URI

#### EC2
- Launch an EC2 instance (e.g., Ubuntu t2.micro)
- Open port `5000` in security group

#### Install Docker on EC2

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
newgrp docker
```

### 3. GitHub Actions Setup

#### Secrets to Add:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION` (e.g., `us-east-1`)
- `AWS_ECR_LOGIN_URI`
- `ECR_REPOSITORY_NAME`

(Go to: Repository → Settings → Secrets → Actions)

### 4. Trigger Deployment

Push changes to the `main` branch. GitHub Actions will:
- Build the Docker image
- Push it to AWS ECR
- SSH into EC2
- Pull & run the container

---

## 📊 Dataset Overview

| Feature                   | Description                                     |
|---------------------------|-------------------------------------------------|
| `hours_studied`           | Total hours spent studying                      |
| `previous_scores`         | Previous exam scores                            |
| `extracurricular_activities` | Binary indicator for extra activities        |
| `sleep_hours`             | Average sleep hours                             |
| `sample_papers_practiced` | Number of practice papers attempted             |
| `score` (Target)          | Final test score to be predicted                |

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

🔗 *Maintained by [Dushyanth142](https://github.com/Dushyanth142)*
