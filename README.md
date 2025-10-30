
---

````markdown
# 🚗 Vehicle Insurance Claim Prediction — End-to-End MLOps Project  

<p align="center">
  <img src="https://img.shields.io/badge/Domain-Machine%20Learning-blue?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/MLOps-End%20to%20End-orange?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Cloud-AWS-yellow?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Database-MongoDB-green?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/CI/CD-GitHub%20Actions-black?style=for-the-badge"/>
</p>

---

## 🧠 Overview

This project is a **complete MLOps pipeline** for automating the lifecycle of a **Vehicle Insurance Claim Prediction System**.  
From **data ingestion and transformation** to **model training, evaluation, and deployment**, everything is automated using **AWS**, **Docker**, and **GitHub Actions**.

The goal?  
To demonstrate mastery over **MLOps architecture, cloud integration, CI/CD, and scalable ML deployment** — exactly what recruiters and real-world systems demand.

---

## ⚙️ Project Workflow

```mermaid
flowchart TD
    A[Template Creation] --> B[Virtual Env & Dependencies]
    B --> C[MongoDB Atlas Setup]
    C --> D[Logging & Exception Handling]
    D --> E[Data Ingestion]
    E --> F[Data Validation]
    F --> G[Data Transformation]
    G --> H[Model Trainer]
    H --> I[AWS Setup]
    I --> J[Model Evaluation & Pusher]
    J --> K[Prediction Pipeline / app.py]
    K --> L[Docker + CI/CD + EC2 Deployment]
````

---

## 🧩 Step-by-Step Setup

### 1️⃣ Project Initialization

```bash
# Create project structure
python template.py

# Setup local packages
# (Refer setup.py and pyproject.toml for package import config)
```

### 2️⃣ Virtual Environment & Dependencies

```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
pip install -r requirements.txt
pip list
```

---

## 🟢 MongoDB Setup (Data Storage)

1. Sign up at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a new **project → cluster → deployment (M0 Tier)**
3. Set up DB user (username/password)
4. Add network access `0.0.0.0/0` (for global access)
5. Get connection string → replace `<username>` and `<password>` → save it
6. Push dataset to MongoDB using Jupyter Notebook (`mongoDB_demo.ipynb`)
7. Verify data in **Atlas > Database > Collections**

---

## 🧾 Logging, Exception & Notebooks

* Implemented **custom logging** and **exception handling** modules for tracking and debugging.
* Verified via `demo.py`.
* Added **EDA & Feature Engineering notebooks** for exploratory analysis.

---

## 📥 Data Ingestion

This stage connects MongoDB → transforms JSON to DataFrame → stores raw data.

* Define constants in `constants/__init__.py`
* MongoDB connection in `configuration/mongo_db_connection.py`
* Data ingestion logic in `components/data_ingestion.py`
* Run:

  ```bash
  export MONGODB_URL="mongodb+srv://<username>:<password>@cluster-url"
  python demo.py
  ```

  or on PowerShell:

  ```bash
  $env:MONGODB_URL = "mongodb+srv://<username>:<password>@cluster-url"
  ```

---

## 📊 Data Validation | 🔄 Data Transformation | 🧠 Model Training

* **Data Validation**: Schema-based validation using `config/schema.yaml`
* **Transformation**: Preprocessing & encoding using `estimator.py`
* **Model Trainer**: Training with robust ML models and saving artifacts

Utility scripts inside `utils/main_utils.py` and entities defined in `entity/`.

---

## ☁️ AWS Cloud Integration

Used **AWS S3**, **IAM**, and **EC2** to build scalable and automated ML infrastructure.

### Setup

1. Create IAM user → `AdministratorAccess`
2. Generate Access/Secret Keys → store as environment variables:

   ```bash
   export AWS_ACCESS_KEY_ID="XXXX"
   export AWS_SECRET_ACCESS_KEY="YYYY"
   ```
3. Create S3 bucket:

   * Name: `my-model-mlopsproj`
   * Region: `us-east-1`
   * Disable “Block Public Access”
4. Update constants:

   ```python
   MODEL_BUCKET_NAME = "my-model-mlopsproj"
   MODEL_PUSHER_S3_KEY = "model-registry"
   MODEL_EVALUATION_CHANGED_THRESHOLD_SCORE = 0.02
   ```
5. Code AWS configuration in:

   * `src/configuration/aws_connection.py`
   * `src/aws_storage/`
   * `entity/s3_estimator.py`

---

## 🧪 Model Evaluation & Deployment

Implements **Model Evaluation**, **Model Pusher**, and **Prediction Pipeline** (`app.py`).

* `/train` → triggers model training
* `/predict` → provides prediction output
* **Static** and **Template** folders manage the web interface.

---

## 🐳 Docker & CI/CD with GitHub Actions

### Docker Setup

```bash
# Build and run Docker image
docker build -t vehicle-insurance-mlops .
docker run -p 5080:5000 vehicle-insurance-mlops
```

### CI/CD Pipeline

1. Configure `.github/workflows/aws.yaml`

2. Create AWS user (`usvisa-user`) for deployment permissions

3. Create ECR repo: `vehicleproj`

4. Setup EC2 instance:

   * Ubuntu 24.04 (t2.medium, 30GB storage)
   * Install Docker:

     ```bash
     curl -fsSL https://get.docker.com -o get-docker.sh
     sudo sh get-docker.sh
     sudo usermod -aG docker ubuntu
     newgrp docker
     ```

5. Connect EC2 → GitHub Runner:

   ```bash
   ./config.sh
   ./run.sh
   ```

6. Add **GitHub Secrets**:

   * `AWS_ACCESS_KEY_ID`
   * `AWS_SECRET_ACCESS_KEY`
   * `AWS_DEFAULT_REGION`
   * `ECR_REPO`

7. Commit → Push → **Pipeline triggers automatically!**

---

## 🌐 Access the Deployed App

1. Open EC2 → Security Group → Edit inbound rules

   * Type: Custom TCP
   * Port: **5080**
   * Source: `0.0.0.0/0`
2. Launch app at:
   **`http://<EC2-public-IP>:5080`**

---

## 🧰 Tech Stack

| Category             | Tools / Frameworks          |
| -------------------- | --------------------------- |
| **Languages**        | Python (3.10)               |
| **Frameworks**       | Flask                       |
| **ML Libraries**     | Scikit-learn, Pandas, NumPy |
| **Database**         | MongoDB Atlas               |
| **Cloud Services**   | AWS S3, EC2, IAM, ECR       |
| **Containerization** | Docker                      |
| **CI/CD**            | GitHub Actions              |
| **Version Control**  | Git & GitHub                |
| **Environment**      | Conda / Virtualenv          |

---

## 🧑‍💻 Project Highlights

✅ Fully Modular Codebase (OOP + Config-driven)
✅ Automated Data Ingestion, Validation, and Transformation
✅ CI/CD Deployment to AWS EC2 with GitHub Actions
✅ Model Registry on AWS S3
✅ Custom Logging and Exception Framework
✅ Dockerized Flask App for Predictions
✅ Real-time MongoDB Integration

---

## 💡 Key Learning Outcomes

* Building **end-to-end MLOps pipelines**
* Integrating **AWS services (IAM, S3, EC2, ECR)**
* Developing **CI/CD workflows using GitHub Actions**
* Managing **data pipelines & artifacts**
* Deploying scalable ML models to production

---

## 🏁 Final Output

Once deployed successfully, your **Vehicle Insurance Prediction Web App** runs seamlessly at port `5080` and can:

* Trigger **model training** from `/training`
* Make **real-time predictions** from `/predict`

---

## 🤝 Connect & Collaborate

If you liked this project, drop a ⭐ on the repo and feel free to connect!

<p align="center">
  <a href="https://www.linkedin.com/in/rajat-singh-6558aa294"><img src="https://img.shields.io/badge/LinkedIn-Rajat%20Singh-blue?style=for-the-badge&logo=linkedin"/></a>
  <a href="mailto:rajat.singh@gmail.com"><img src="https://img.shields.io/badge/Email-Contact%20Me-red?style=for-the-badge&logo=gmail"/></a>
</p>

---

> 🚀 *"From local notebooks to production-grade deployment — this project is a complete MLOps journey!"*

```
