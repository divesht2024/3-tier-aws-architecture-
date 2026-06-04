
# 🏗️ Production-Grade 3-Tier Architecture on AWS

A production-ready, fault-tolerant 3-tier AWS infrastructure deployed across **2 Availability Zones** with isolated public and private subnets for web, application, and database tiers — following AWS Well-Architected Framework best practices.

---

---

## 🎯 What This Project Demonstrates

- **High Availability** — Infrastructure spread across 2 Availability Zones (us-east-1a, us-east-1b)
- **Fault Tolerance** — No single point of failure at any tier
- **Security** — Least-privilege Security Groups, private subnets for app and database tiers
- **Scalability** — Auto Scaling Groups at web and app tiers
- **Production Readiness** — Multi-AZ RDS, internal ALB, CloudWatch monitoring

---

## ☁️ AWS Services Used

| Service | Tier | Purpose |
|---------|------|---------|
| Amazon VPC (10.0.0.0/16) | All | Isolated private network |
| Internet Gateway | Web | Enables internet access |
| Application Load Balancer (External) | Web | Routes internet traffic to Web Tier EC2s |
| Amazon EC2 + ASG | Web | Web servers in public subnets (10.0.1.0/24, 10.0.4.0/24) |
| Application Load Balancer (Internal) | App | Routes traffic from Web Tier to App Tier |
| Amazon EC2 + ASG | App | App servers in private subnets (10.0.2.0/24, 10.0.5.0/24) |
| Amazon RDS (Primary + Read Replica) | DB | MySQL in private subnets (10.0.3.0/24, 10.0.6.0/24) |
| NAT Gateway | All | Outbound internet for private subnets |
| Route Tables | All | Controls traffic routing per subnet |
| Security Groups | All | Stateful firewall per tier |
| AWS IAM | All | Least-privilege roles per tier |
| Amazon CloudWatch | All | Monitoring, alarms, dashboards |
| AWS Auto Scaling | Web + App | Dynamic scaling based on demand |

---

## 🔄 Request Flow

```
Internet Users
      ↓
Internet Gateway
      ↓
External ALB (DNS: app.example.com)
  • Terminates TLS (HTTPS)
  • Health checks
  • Routes to Web Tier
      ↓
┌─────────────────────────────────┐
│         Web Tier (Public)       │
│  EC2 Web Server 1 (AZ1)        │
│  EC2 Web Server 2 (AZ2)        │
│  Both in Auto Scaling Group     │
└─────────────────────────────────┘
      ↓
Internal ALB
  • Internal-facing
  • Distributes traffic to App Tier
  • Improves fault tolerance
      ↓
┌─────────────────────────────────┐
│        App Tier (Private)       │
│  EC2 App Server 1 (AZ1)        │
│  EC2 App Server 2 (AZ2)        │
│  Both in Auto Scaling Group     │
└─────────────────────────────────┘
      ↓
┌─────────────────────────────────┐
│      Database Tier (Private)    │
│  Amazon Aurora Primary (Writer) │
│  Amazon Aurora Read Replica     │
│  Multi-AZ deployment            │
└─────────────────────────────────┘
      ↓
Response back to User
```

---
## 🌐 Network Architecture

| Subnet | CIDR | AZ | Tier |
|--------|------|----|------|
| Public Subnet 1 | 10.0.1.0/24 | ap-south-1a | Web |
| Public Subnet 2 | 10.0.4.0/24 | ap-south-1b | Web |
| Private Subnet 1 | 10.0.2.0/24 | ap-south-1a | App |
| Private Subnet 2 | 10.0.5.0/24 | ap-south-1b | App |
| Private Subnet 3 | 10.0.3.0/24 | ap-south-1a | Database |
| Private Subnet 4 | 10.0.6.0/24 | ap-south-1b | Database |

**Routing:**
- Public subnets → Internet Gateway (0.0.0.0/0)
- Private subnets → NAT Gateway (0.0.0.0/0)

---

## 🔐 Security Architecture

```
Internet → External ALB (HTTPS only)
                ↓
        Web Tier EC2s
        (SG: allow 80/443 from ALB only)
                ↓
        Internal ALB
                ↓
        App Tier EC2s
        (SG: allow traffic from Web Tier SG only)
                ↓
        RDS Database
        (SG: allow 3306 from App Tier SG only)
```

- ✅ No direct public access to App or Database tiers
- ✅ Security Groups enforce least-privilege per tier
- ✅ IAM roles assigned per tier — no hardcoded credentials
- ✅ Data encrypted at rest (AES-256) and in transit (TLS)
- ✅ NAT Gateway for outbound-only internet from private subnets

---

## 📊 High Availability & Fault Tolerance

| Component | HA Mechanism |
|-----------|-------------|
| Web Tier | ASG across 2 AZs — auto scale-out from 2 to 4 instances |
| App Tier | ASG across 2 AZs — auto scale-out based on CPU |
| Database | Aurora Primary (Writer) + Read Replica across 2 AZs |
| Load Balancing | External ALB + Internal ALB with health checks |
| Monitoring | CloudWatch alarms on CPU, memory, request metrics with SNS alerts — sub-5-minute detection |

---

## ⚙️ Key Features

- **Dual ALB setup** — External ALB for internet traffic, Internal ALB for web-to-app routing
- **Auto Scaling** — Dynamic scale-out at both web and app tiers based on demand
- **Multi-AZ RDS** — Aurora Primary (Writer) + Read Replica for read scalability
- **Encryption** — Data encrypted at rest (AES-256) and in transit (TLS)
- **Automated backups** — RDS automated backups and cross-region DR capability
- **CloudWatch monitoring** — Dashboards, alarms, SNS alerts across all tiers
- **Full-stack deployment** — End-to-end validated with a full-stack web application

---

---

## 📸 Screenshots

| Component | Screenshot |
|-----------|-----------|
| VPC Configuration | screenshots/vpc.png |
| External ALB | screenshots/external-alb.png |
| Internal ALB | screenshots/internal-alb.png |
| Web Tier EC2s | screenshots/web-ec2.png |
| App Tier EC2s | screenshots/app-ec2.png |
| RDS Primary + Replica | screenshots/rds.png |
| Auto Scaling Groups | screenshots/asg.png |
| CloudWatch Dashboard | screenshots/cloudwatch.png |
| Security Groups | screenshots/security-groups.png |
| Full-stack App Running | screenshots/app-output.png |

---

## 🏆 Key Achievements

- ✅ Zero single point of failure across all three tiers
- ✅ Automatic scale-out from 2 to 4 EC2 instances under load
- ✅ Sub-5-minute issue detection via CloudWatch + SNS alerts
- ✅ Full-stack web application deployed and validated end-to-end
- ✅ Production-grade security with least-privilege access per tier

---

## 👨‍💻 Author

**Divesh M. Tayade**
- 🐙 GitHub: [@divesht2024](https://github.com/divesht2024)
- 💼 LinkedIn: [linkedin.com/in/divesh-tayade](https://www.linkedin.com/in/divesh-tayade-4a010124a/)
- 📧 diveshtayade20@gmail.com

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
