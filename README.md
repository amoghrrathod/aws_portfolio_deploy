# ☁️ AWS EC2 Web App Deployment with Automated Shutdown & Cost Governance

## 📌 Overview

This project showcases a complete deployment of a personal web application on AWS, using an **EC2 instance**, **custom VPC**, and **IAM role-based access**, while incorporating **cost control mechanisms** and **automated resource scheduling** to manage cloud usage efficiently.

The project was developed as part of a self-initiated cloud learning journey in May 2024 and demonstrates a hands-on understanding of AWS compute, security, identity, and cost optimization services.

---

## 🏗️ Architecture Summary

- **Compute:** Amazon EC2 (Amazon Linux, Free Tier)
- **Networking:** Custom VPC with dedicated security groups
- **Access Management:** IAM role with scoped EC2 permissions
- **SSH Access:** Custom PEM key pair for secure login
- **Web Server:** NGINX for serving static website content
- **Storage:** Amazon EBS (Free Tier)
- **Monitoring & Governance:** AWS Budgets, SNS notifications, and Systems Manager automation

## 🖼️ Architecture Diagram

![AWS Architecture Diagram](https://github.com/user-attachments/assets/648fd733-f42f-40ed-9d42-f0c476f8c9b1)

---

## ⚙️ Implementation Steps

### 1. EC2 Instance Launch
- Deployed a Free Tier Amazon Linux EC2 instance with default Amazon EBS storage.
- Configured security group rules to allow inbound traffic on ports:
  - **22** for SSH
  - **80** for HTTP
  - **443** for HTTPS
- Deployed within a **custom VPC** for logical network isolation.

### 2. IAM Role Creation
- Created a scoped IAM role with permissions for EC2 management.
- Assigned the role to the EC2 instance for **least-privilege access** using **instance profiles**.
- Role was added to a group with access to:
  - Start/Stop/Terminate EC2 instances
  - Monitor usage metrics

### 3. Secure Access & Deployment
- Generated a PEM key pair to SSH into the instance.
- Used `scp` to securely transfer website files to the instance.
- Performed system updates with `dnf update && dnf upgrade`.
- Installed and configured **NGINX**.
  - Bound the server block to the public IP of the instance.
  - Deployed website files to `/var/www/html/`.

### 4. Cost Monitoring & Auto-Termination
- Configured **AWS Budgets** to trigger alerts at **$0.0001 usage**.
- Set up **SNS notification topic** linked to budget threshold alerts.
- Utilized **AWS Systems Manager > Quick Setup > Resource Scheduling** to:
  - Create a scheduled shutdown automation rule.
  - Ensure EC2 instance auto-terminates when **95% of Free Tier usage** is reached.
- Verified receipt of **email notification** confirming instance shutdown.

---

## 🧠 Key Learnings

- End-to-end EC2 instance provisioning with proper access, networking, and deployment.
- Applied the **principle of least privilege** via IAM.
- Enforced **cost governance** through budget thresholds and auto-shutdown.
- Gained experience with **Systems Manager**, **SNS**, and **resource automation**.
- Hands-on exposure to managing Linux servers, NGINX, and secure file transfers.

---

## 📸 Potential Additions

While this project is no longer live (resources were terminated post deployment), the following can be added to the repository:

- ✅ AWS architecture diagram (draw.io or Lucidchart)
- ✅ Sample screenshots of EC2 dashboard, IAM roles, Budgets, and SNS
- ✅ Sample `nginx.conf` config
- ✅ Example of budget alert JSON or automation script (if manually created)

---

## 🧾 Disclaimer

This project was implemented for educational and personal portfolio purposes. All resources were terminated after completion to avoid billing beyond AWS Free Tier limits.

---

## 📌 Tags

`AWS` `EC2` `IAM` `Systems Manager` `NGINX` `Cloud Cost Optimization` `DevOps` `VPC` `Budget Alerts` `SCP` `Automation` `Infrastructure`
