# # Cloud Auto-Scaling and Security Implementation (GCP)

##  Project Overview

This project demonstrates the deployment of a Virtual Machine (VM) in **Google Cloud Platform (GCP)** with:

- CPU-based Auto Scaling
- Managed Instance Group (MIG)
- IAM Role-Based Access Control
- Firewall Configuration (Allow + Deny Rules)
- Automated Infrastructure using Startup Scripts

The system dynamically scales VM instances based on workload while maintaining strict security controls.

---

##  Objective

To implement scalable and secure cloud infrastructure using:

- Compute Engine
- Managed Instance Groups
- Auto-scaling policies
- IAM for restricted access
- VPC firewall rules

---

## ☁️ Cloud Platform Used

- **Google Cloud Platform (GCP)**
- **Service:** Compute Engine

---

## 🏗️ Architecture Overview

The architecture consists of:

- Internet Users
- VPC Firewall Rules
- Managed Instance Group (MIG)
- CPU-Based Auto Scaling Policy
- Multiple VM Instances (Nginx Web Server)
- IAM Role-Based Access Control

📌 Architecture Diagram:

`architecture/architecture.png`

---

## ⚙️ Implementation Steps

### 1️⃣ Instance Template

An instance template was created with:

- Machine Type: `e2-micro`
- OS: Debian Linux
- Firewall: Allow HTTP
- Startup Script for Nginx automation

The template ensures all auto-scaled instances are identical.

---

### 2️⃣ Startup Script (Automation)

File: `scripts/startup-script.sh`

The script:

- Updates system packages
- Installs Nginx
- Starts and enables service
- Displays:
  - Hostname
  - Internal IP
  - Instance creation time

This helps visually verify auto-scaling.

---

### 3️⃣ Managed Instance Group (MIG)

Configuration:

- Minimum Instances: 1
- Maximum Instances: 3
- Auto-healing enabled

The MIG maintains identical VM instances and ensures high availability.

---

### 4️⃣ Auto Scaling Configuration

- Metric: CPU Utilization
- Target CPU: 60%

Behavior:

- If CPU > 60% → New VM instances created
- If CPU drops → Extra instances removed

This ensures elastic resource allocation and cost optimization.

---

## 🔥 Testing Auto-Scaling

To simulate high workload:

```bash
sudo apt install stress -y
stress --cpu 2 --timeout 300
