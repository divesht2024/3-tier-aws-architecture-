# 🚀 Basic 3-Tier AWS Architecture on AWS

This project demonstrates the design and implementation of a **Basic 3-Tier Architecture on AWS**.

The infrastructure separates the application into three different network tiers to improve **security, maintainability, scalability, and performance**.

- **Tier 1 – Presentation Layer:** Amazon EC2 deployed in a Public Subnet  
- **Tier 2 – Application Layer:** Amazon EC2 deployed in a Private Subnet  
- **Tier 3 – Database Layer:** Amazon RDS MySQL deployed in a Private Subnet  

This architecture follows cloud best practices by allowing public access only to the frontend server while keeping backend and database resources isolated from direct internet exposure.

---

## ☁️ AWS Services Used

| Service | Purpose |
|--------|---------|
| Amazon VPC | Isolated private network |
| Public Subnet | Hosts internet-facing Frontend EC2 |
| Private Subnet | Hosts Backend EC2 and RDS |
| Internet Gateway | Enables internet access |
| NAT Gateway | Provides outbound internet for private subnet |
| Route Tables | Controls network traffic |
| Amazon EC2 | Frontend / Backend servers |
| Amazon RDS | Managed relational database |
| Security Groups | Firewall and access control |

---

## 🔄 Request Flow

```text
User Browser
   ↓
Internet
   ↓
Internet Gateway
   ↓
Frontend EC2 (Presentation Layer)
   ↓
Backend EC2 (Application Layer)
   ↓
Amazon RDS MySQL (Database Layer)
   ↓
Response to User
```

🔐 Security Architecture

✔ Frontend server deployed in Public Subnet
✔ Backend server deployed in Private Subnet
✔ Database deployed in Private Subnet
✔ No direct public access to Backend or RDS
✔ NAT Gateway used for outbound internet from private subnet
✔ Security Groups restrict inbound/outbound traffic
✔ Application and database layers are logically separated

⚙️ Key Features Implemented

Custom Amazon VPC
Public and Private Subnet Design
Frontend Web Hosting on EC2
Backend Application Hosting on EC2
RDS Database Connectivity
Secure Network Segmentation
Internet Gateway Integration
NAT Gateway Configuration
Controlled Security Group Rules

📚 Skills Demonstrated

AWS Cloud Architecture Design
Networking Fundamentals (VPC/Subnets)
Compute Deployment (EC2)
Multi-Tier Application Deployment
Database Integration (RDS)
Security Best Practices
Troubleshooting & Connectivity
Cloud Project Documentation

📸 Screenshots

Frontend EC2 Running State
Backend EC2 Running State
RDS Instance Dashboard
VPC Configuration
Route Tables
NAT Gateway Status
Security Group Rules
Frontend Working Output
Successful Backend Connection
Successful DB Connection

📂 Repository Structure

3-tier-aws-architecture/
│── frontend/
│── backend/
│── database/
│── screenshots/
│── architecture/
│── README.md


👨‍💻 Author
DIVESH M. TAYADE
AWS | Cloud Engineer | DevOps Enthusiast
