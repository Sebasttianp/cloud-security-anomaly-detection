# Cloud Security Anomaly Detection Platform

> 🚧 **Planned** — This repository currently contains the project plan only. No code, data, or notebooks have been committed yet. Phases are checked off as the work is added here.

A machine learning–based anomaly detection platform that analyzes cloud security audit logs to identify suspicious activity. Built to simulate the kind of detection engineering work done in real cloud security and SOC environments.

---

## 🎯 What This Project Does

Cloud environments generate thousands of audit log events every day — logins, API calls, resource changes, policy updates. Most are normal. A few aren't. This platform uses an unsupervised machine learning model to automatically surface the ones that look suspicious, and explains *why* they were flagged.

**Real-world use cases this mirrors:**
- Detecting unusual login behavior (odd hours, unfamiliar IPs, repeated failures)
- Flagging unexpected resource deletions or policy changes
- Identifying privilege escalation patterns in IAM audit logs
- Surfacing low-and-slow attacks that rule-based systems miss

---

## 🏗️ Architecture

```
Cloud Audit Logs (synthetic OCI/Azure-style)
        ↓
Data Preprocessing & Feature Engineering
        ↓
Isolation Forest ML Model (unsupervised anomaly detection)
        ↓
SHAP Explainability (why was this flagged?)
        ↓
FastAPI REST Endpoint (POST /predict)
        ↓
Docker Container → Deployed on Oracle Cloud / Azure
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3.10 |
| ML Model | Isolation Forest (scikit-learn) |
| Explainability | SHAP |
| API | FastAPI |
| Containerization | Docker |
| Cloud Deployment | Oracle Cloud Infrastructure (OCI) or Azure |
| Data | Synthetic cloud audit logs (Faker + custom generator) |

---

## 📁 Planned Project Structure

None of these files are in the repository yet.

```
cloud-security-anomaly-detection/
├── data/
│   ├── generate_logs.py          # Synthetic log generator
│   ├── raw_cloud_audit_logs.csv  # Generated raw logs
│   └── processed_cloud_logs.csv  # Cleaned & encoded logs
├── notebooks/
│   ├── 01_data_preprocessing.ipynb
│   └── 02_anomaly_detection.ipynb
├── app/
│   └── main.py                   # FastAPI REST API
├── model/
│   └── isolation_forest.pkl      # Trained model
├── docker/
│   └── Dockerfile
├── screenshots/
└── requirements.txt
```

---

## 🔬 ML Approach — Why Isolation Forest?

Most security anomaly detection problems are **unsupervised** — you don't have labeled data telling you which events are attacks. Isolation Forest is ideal here because it:

- Requires no labeled training data
- Is designed specifically for anomaly detection
- Handles high-dimensional log data well
- Is fast and explainable — perfect for security use cases
- Maps directly to how real SIEM and UEBA tools work under the hood

---

## 🚦 Build Progress

- [ ] Phase 1 — Project setup & synthetic log generation
- [ ] Phase 2 — ML model training (Isolation Forest)
- [ ] Phase 3 — SHAP explainability
- [ ] Phase 4 — FastAPI REST endpoint
- [ ] Phase 5 — Docker containerization
- [ ] Phase 6 — Cloud deployment (OCI / Azure)
- [ ] Phase 7 — Final README, screenshots & polish

---

## 📡 API (Coming in Phase 4)

```http
POST /predict
Content-Type: application/json

{
  "timestamp": 1700000000,
  "user": "admin",
  "action": "delete_vm",
  "region": "eu-frankfurt-1",
  "source_ip": "192.168.1.100",
  "success": false
}
```

**Response:**
```json
{
  "anomaly_score": -0.42,
  "is_anomaly": true,
  "explanation": "Unusual action (delete_vm) from unfamiliar region with failed auth"
}
```

---

## 💡 Why This Project Matters

Detection engineering is one of the fastest-growing areas in cloud security. The ability to build systems that automatically surface suspicious behavior — and explain it — is exactly what security teams are hiring for. This project demonstrates:

- Understanding of unsupervised ML applied to security
- Ability to work with real-world log data formats
- Full-stack thinking: from raw data to deployed API
- Explainable AI — critical for security use cases where analysts need to understand *why* something was flagged

---

## 🔗 Related Projects

- [Azure Secure Network Lab](https://github.com/Sebasttianp/azure-secure-network-lab) — VNet segmentation and NSG configuration
- [Cloud Security Labs](https://github.com/Sebasttianp/cloud-security-labs) — Azure, Entra ID, IAM, and MFA
