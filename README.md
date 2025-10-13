# 🚀 MLOps Vehicle Insurance Prediction Project

> A comprehensive end-to-end machine learning operations pipeline demonstrating production-grade ML engineering practices with cloud-native architecture and automated CI/CD deployment.

---

## 📋 Overview

This project showcases a complete MLOps ecosystem built to handle real-world machine learning workflows. From data ingestion through model deployment, every component is engineered for scalability, reliability, and reproducibility. This is a showcase of industry best practices in machine learning engineering.

---

## 🏗️ Architecture & Components

### **Data Pipeline**
- **Data Ingestion**: Automated extraction and transformation of raw data from MongoDB Atlas into structured formats
- **Data Validation**: Schema validation and data quality checks using configuration-driven validation rules
- **Data Transformation**: Feature engineering and preprocessing with scikit-learn integration
- **Model Training**: Automated model training pipeline with hyperparameter optimization

### **Model Management**
- **Model Evaluation**: Comprehensive model performance tracking with threshold-based quality gates
- **Model Registry**: Centralized model storage and versioning using AWS S3
- **Model Pusher**: Automated model promotion to production when quality benchmarks are met

### **Prediction Pipeline**
- **Real-time Inference**: FastAPI-based prediction service for online predictions
- **Web Interface**: User-friendly Flask/HTML templates for model interaction

---

## 🛠️ Tech Stack

### Core Technologies
- **Language**: Python 3.10
- **ML Framework**: scikit-learn
- **Data Processing**: Pandas, NumPy
- **Orchestration**: Custom Python pipelines

### Database & Storage
- **Database**: MongoDB Atlas (NoSQL, cloud-hosted)
- **Object Storage**: AWS S3 (model registry, artifacts)
- **Data Format**: Key-value documents, DataFrames, Pickle serialization

### Cloud & DevOps
- **Cloud Platform**: Amazon Web Services (AWS)
  - **EC2**: Ubuntu servers for application hosting
  - **ECR**: Docker image registry for containerized applications
  - **IAM**: Identity and access management
  - **S3**: Scalable object storage
- **Containerization**: Docker & Docker Compose
- **CI/CD**: GitHub Actions with self-hosted runners
- **Infrastructure**: AWS EC2 (T2 Medium instance)

### Development & Environment
- **Environment Management**: Conda virtual environments
- **Configuration Management**: YAML schemas and constants
- **Version Control**: Git & GitHub
- **Logging & Monitoring**: Structured logging throughout pipeline

---

## 🚀 Quick Start

### Prerequisites
```bash
# Create and activate conda environment
conda create -n vehicle python=3.10 -y
conda activate vehicle

# Install dependencies
pip install -r requirements.txt
```

### Setup MongoDB
1. Sign up to **MongoDB Atlas**
2. Create a cluster (M0 free tier recommended)
3. Configure database user and network access (0.0.0.0/0)
4. Obtain connection string from Drivers section

### Configure Environment
```bash
# On Bash/Terminal
export MONGODB_URL="mongodb+srv://<username>:<password>......"

# Verify
echo $MONGODB_URL
```

### Run Pipeline
```bash
python demo.py
```

---

## 📊 Pipeline Workflow

### **Data Ingestion**
```
MongoDB Atlas → Fetch Data → Transform to DataFrame → Store Artifacts
```
- Connects to MongoDB using PyMongo
- Converts document-based data to tabular format
- Saves intermediate artifacts for reproducibility

### **Data Validation**
```
Raw Data → Schema Validation → Quality Checks → Validation Report
```
- Validates data types and structure against schema.yaml
- Detects missing values and anomalies
- Generates detailed validation reports

### **Data Transformation**
```
Validated Data → Feature Engineering → Preprocessing → Transformed Dataset
```
- Applies statistical transformations
- Encodes categorical variables
- Scales numerical features

### **Model Training**
```
Transformed Data → Train/Test Split → Model Fitting → Model Artifact
```
- Trains multiple model variants
- Evaluates on held-out test set
- Saves best-performing model

### **Model Evaluation**
```
New Model ⚖️ Current Model → Performance Comparison → Quality Gate
```
- Compares new model against production baseline
- Applies threshold-based decision rules (default: 2% improvement required)
- Determines promotion eligibility

### **Model Deployment**
```
Approved Model → Docker Container → ECR Registry → EC2 Deployment → Live Inference
```
- Containerizes application
- Pushes to AWS ECR
- Auto-deploys to EC2 via GitHub Actions

---

## 🏢 AWS Integration

### IAM Setup
- Created dedicated IAM users with AdministratorAccess
- Managed credentials via environment variables
- Region: us-east-1

### S3 Bucket Configuration
- **Bucket Name**: my-model-mlopsproj
- **Purpose**: Model registry and artifact storage
- **Access**: Programmatic access via boto3

### EC2 Deployment
- **Instance Type**: t3.micro
- **AMI**: Ubuntu Server 24.04 LTS
- **Storage**: 30GB
- **Docker Enabled**: Pre-configured container runtime

### ECR Repository
- **Repo Name**: vehicleproj
- **Purpose**: Docker image versioning and management
- **Integration**: Automated pushes via GitHub Actions

---

## 🔄 CI/CD Pipeline

### GitHub Actions Workflow
Automated deployment triggered on every commit:
1. **Build**: Docker image creation with optimized layers
2. **Push**: Image pushed to AWS ECR with version tags
3. **Deploy**: Automatic deployment to self-hosted EC2 runner

### Self-Hosted Runner
- GitHub-to-EC2 integration for seamless CI/CD
- Runs Docker containers on Ubuntu 24.04
- Monitors job queue and executes workflows

### Secrets Management
```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_DEFAULT_REGION
ECR_REPO
```

### Port Configuration
- **Application Port**: 5080 (custom TCP)
- **Security**: 0.0.0.0/0 for accessibility

---

## 📁 Project Structure

```
vehicle-proj/
├── src/
│   ├── components/
│   │   ├── data_ingestion.py
│   │   ├── data_validation.py
│   │   ├── data_transformation.py
│   │   ├── model_trainer.py
│   │   ├── model_evaluation.py
│   │   └── model_pusher.py
│   ├── configuration/
│   │   ├── mongo_db_connections.py
│   │   ├── aws_connection.py
│   │   └── constants/__init__.py
│   ├── data_access/
│   │   └── proj1_data.py
│   ├── aws_storage/
│   │   └── s3_estimator.py
│   ├── entity/
│   │   ├── config_entity.py
│   │   ├── artifact_entity.py
│   │   ├── estimator.py
│   │   └── s3_estimator.py
│   ├── pipeline/
│   │   └── training_pipeline.py
│   └── utils/
│       └── main_utils.py
├── config/
│   └── schema.yaml
├── notebook/
│   └── mongoDB_demo.ipynb
├── static/
├── templates/
├── Dockerfile
├── docker-compose.yml
├── .github/workflows/
│   └── aws.yaml
├── .gitignore
├── requirements.txt
├── setup.py
├── pyproject.toml
├── app.py
└── demo.py
```

---

## 🔐 Security & Best Practices

✅ **Environment Variables**: Sensitive credentials stored securely  
✅ **IAM Roles**: Least-privilege access control  
✅ **Network Security**: VPC and security group configurations  
✅ **Version Control**: Git ignore for artifacts and secrets  
✅ **Containerization**: Reproducible, isolated runtime environments  
✅ **Code Modularization**: Separation of concerns across components  

---

## 📈 Key Features

🎯 **End-to-End Automation**: From data ingestion to model serving  
🔄 **Production-Grade Pipelines**: Modular, testable, and maintainable  
☁️ **Cloud-Native Architecture**: Fully leverages AWS services  
🐳 **Containerized Deployment**: Docker for consistency across environments  
🤖 **ML Best Practices**: Model validation, evaluation gates, versioning  
⚡ **Scalable Infrastructure**: Ready for production workloads  
📊 **Comprehensive Logging**: Audit trails and debugging information  

---

## 🚦 Model Quality Gates

The pipeline enforces quality standards before production deployment:

| Metric | Threshold | Purpose |
|--------|-----------|---------|
| Model Improvement | ≥ 2% | Ensures better performance than baseline |
| Data Validation | 100% | Prevents bad data from training |
| Schema Compliance | Strict | Maintains data integrity |

---

## 📞 Contact & Support

For questions or collaboration opportunities, feel free to reach out!

---

**Built with ❤️ using MLOps best practices | Designed to impress | Production-ready**