# LogSense 🔍🤖

> An end-to-end machine learning system for automatically classifying infrastructure logs and error messages.

## Overview

**LogSense** is an AI-powered infrastructure log classification system designed to automatically identify and categorize errors from application logs, servers, databases, containers, and network services.

Infrastructure teams often deal with thousands of log messages across multiple services. Finding and categorizing important errors manually can be slow and difficult. LogSense uses machine learning and natural language processing to classify log messages into meaningful error categories.

The project is designed as a practical exploration of the complete AI engineering lifecycle:

```text
Data → Preprocessing → Training → Evaluation → Deployment → Monitoring
```

Rather than relying solely on an external LLM API, LogSense focuses on training and deploying machine learning models for a specific infrastructure intelligence task.

---

## ✨ Features

### Initial Version

* Classify infrastructure log messages into predefined categories
* Return prediction confidence scores
* Compare a traditional machine learning baseline against a transformer-based model
* Expose the trained model through a REST API
* Run the application using Docker

### Planned Features

* Log anomaly detection
* Multi-label classification
* Model confidence analysis
* User feedback collection for incorrect predictions
* Automated dataset improvement pipeline
* Experiment tracking
* Model versioning
* Prediction monitoring dashboard
* Real-time log stream classification

---

## 🧠 Classification Categories

The initial version of LogSense will classify logs into categories such as:

| Category               | Example                                             |
| ---------------------- | --------------------------------------------------- |
| `DATABASE_ERROR`       | `Connection refused while connecting to PostgreSQL` |
| `NETWORK_ERROR`        | `Network timeout while contacting upstream service` |
| `AUTHENTICATION_ERROR` | `Invalid authentication token`                      |
| `MEMORY_ERROR`         | `Process terminated due to out of memory`           |
| `APPLICATION_ERROR`    | `Unhandled exception in application`                |
| `CONTAINER_ERROR`      | `Container exited with non-zero status`             |
| `DISK_ERROR`           | `No space left on device`                           |

The categories may evolve as the dataset grows and the model is evaluated. Real data has a habit of disagreeing with our beautifully organized plans.

---

## 🏗️ System Architecture

```text
                  ┌───────────────────────┐
                  │   Log / Error Input   │
                  └───────────┬───────────┘
                              │
                              ▼
                  ┌───────────────────────┐
                  │   Text Preprocessing  │
                  └───────────┬───────────┘
                              │
                              ▼
                  ┌───────────────────────┐
                  │  Classification Model │
                  │                       │
                  │  Baseline / Transformer
                  └───────────┬───────────┘
                              │
                              ▼
                  ┌───────────────────────┐
                  │ Prediction + Confidence│
                  └───────────┬───────────┘
                              │
                              ▼
                  ┌───────────────────────┐
                  │       FastAPI API     │
                  └───────────────────────┘
```

---

## 🤖 Machine Learning Approach

LogSense will begin with a traditional machine learning baseline before introducing deep learning.

### Baseline Model

The first model will use:

* **TF-IDF Vectorization**
* **Logistic Regression**

This provides a fast and interpretable baseline.

### Transformer Model

The second iteration will fine-tune a pretrained transformer model for text classification.

Possible models include:

* DistilBERT
* BERT
* Other lightweight transformer models suitable for classification

The performance of the transformer model will be compared against the baseline using the same evaluation dataset.

---

## 📊 Model Evaluation

Models will be evaluated using metrics such as:

* Accuracy
* Precision
* Recall
* F1 Score
* Confusion Matrix
* Inference Latency

Example comparison:

| Model                        | Accuracy | F1 Score | Avg. Latency |
| ---------------------------- | -------: | -------: | -----------: |
| TF-IDF + Logistic Regression |      TBD |      TBD |          TBD |
| Fine-tuned Transformer       |      TBD |      TBD |          TBD |

The goal is not simply to achieve the highest possible accuracy. Model size, inference speed, and deployment cost are also important considerations for real-world AI systems.

---

## 📁 Project Structure

```text
logsense/
│
├── data/
│   ├── raw/                    # Original datasets
│   ├── processed/              # Cleaned and processed datasets
│   └── README.md
│
├── notebooks/                  # Data exploration and experiments
│
├── src/
│   ├── data/
│   │   ├── preprocessing.py
│   │   └── dataset.py
│   │
│   ├── models/
│   │   ├── baseline.py
│   │   ├── transformer.py
│   │   └── evaluate.py
│   │
│   └── utils/
│
├── api/
│   ├── main.py
│   ├── schemas.py
│   └── model_service.py
│
├── tests/
│
├── models/                     # Saved trained models
│
├── pyproject.toml
├── uv.lock
├── Dockerfile
├── docker-compose.yml
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

* Python 3.10 or newer
* uv (UV tool for virtual environment management)
* Docker (optional)
* Git

### Clone the Repository

```bash
git clone https://github.com/KavinduPramod/LOGSENSE.git
cd LOGSENSE
```
### Install UV tool if not already installed

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### add uv to path
open powershell and run the following command to add uv to your path
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```
### verify uv installation
```bash
uv --version
```
### Create a Virtual Environment and Install Dependencies

```bash
uv sync
```

### Install Dependencies

```bash
uv add <package_name>
```

---

## 🔌 API Usage

Once the API is running:

```bash
uv run uvicorn api.main:app --reload
```

Send a prediction request:

### Request

```http
POST /predict
Content-Type: application/json
```

```json
{
  "log": "ERROR: Connection refused while connecting to the database"
}
```

### Response

```json
{
  "category": "DATABASE_ERROR",
  "confidence": 0.94
}
```

---

## 🐳 Running with Docker

```bash
docker build -t logsense .
docker run -p 8000:8000 logsense
```

The API will then be available at:

```text
http://localhost:8000
```

## 🎯 Learning Goals

LogSense is designed to provide practical experience with:

* Machine Learning
* Natural Language Processing
* Transformer Models
* Model Fine-Tuning
* Dataset Engineering
* Model Evaluation
* REST API Development
* Docker
* Model Deployment
* MLOps Fundamentals

---

## 🛠️ Technology Stack

| Area            | Technologies              |
| --------------- | ------------------------- |
| Language        | Python                    |
| ML Baseline     | Scikit-learn              |
| Deep Learning   | PyTorch                   |
| Transformers    | Hugging Face Transformers |
| API             | FastAPI                   |
| Data Processing | Pandas, NumPy             |
| Deployment      | Docker                    |
| Testing         | Pytest                    |
| CI/CD           | GitHub Actions            |

---

## 📌 Project Philosophy

The goal of LogSense is to build an AI system incrementally and understand each stage of the machine learning lifecycle.

The project follows a simple principle:

> **Build a working baseline first. Improve it using data and evaluation, not assumptions.**

Each version of the project should be measurable, reproducible, and explainable.

---

## 📈 Current Status

🚧 **Currently in early development.**

The first milestone is to build and evaluate a baseline machine learning model for infrastructure log classification.

---

## 🤝 Contributing

This is currently a personal learning and portfolio project. Contributions, discussions, and suggestions are welcome as the project develops.

---

## 📄 License

This project is released under the MIT License.

---

## 👨‍💻 Author

**RobinsoN**

Built as a hands-on exploration of practical AI engineering, machine learning, NLP, and MLOps.
