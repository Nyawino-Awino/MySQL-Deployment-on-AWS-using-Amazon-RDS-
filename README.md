# 🚀 Secure MySQL Deployment on AWS using Amazon RDS in a Custom VPC.
📌 Project Overview
Designed and deployed a secure, highly available MySQL database architecture on Amazon Web Services using Amazon RDS within a custom-built VPC.
The goal is to build a secure, production-style architecture where:
  - The database is not exposed to the internet 
  - Access is controlled through a web server (bastion host) 
  - The setup supports high availability using Multi-AZ deployment
---
## 🧠 Why Use a VPC?
A VPC is critical because it allows you to:
- 🔐 Isolate your database in private subnets
- 🎛️ Control traffic using security groups and route tables
- 🛡️ Add an extra security layer with Network ACLs
- 🌍 Enable Multi-AZ deployments for high availability
---
## 🏗️ Architecture Overview
![Architecture Diagram](architecture/architecture.png)

---
## 🧱 Step 1: Create a VPC
Go to the **AWS Management Console**
Search for **VPC** and open the dashboard
Click **Create VPC**
Configure:
- Name: *RDS-VPC*
- IPv4 CIDR: *10.0.0.0/16*
- IPv6: *None*
- Tenancy: *Default*

Click **Create VPC**

✅ Your network foundation is now ready.

---
## 🔐 Step 2: Create Security Groups
Security groups act as **virtual firewalls**.

🔹 Web Server Security Group
Go to **Security Groups** → Create

Configure:
- Name: *Web-Server-SG*
- VPC: *RDS-VPC*

**Inbound Rules**:
- HTTP (80) → Anywhere (0.0.0.0/0)
- SSH (22) → Anywhere (0.0.0.0/0)

👉 This allows web access and SSH login

🔹 RDS Database Security Group

Create another security group:
- Name: *RDS-DB-SG*
- VPC: *RDS-VPC*
  
**Inbound Rule**:
- MySQL (3306)
- Source: Web Server Security Group
  
👉 This ensures:

✔ Only the web server can access the database

❌ No direct public access

---
## 🌐 Step 3: Create Subnets
You will create **4 subnets** across **2 Availability Zones**.
 
- Public Subnet 1	   | 10.0.0.0/24	|    AZ-1
- Private Subnet 1	 | 10.0.1.0/24	|   AZ-1
- Public Subnet 2	   | 10.0.2.0/24	|   AZ-2
- Private Subnet 2	 |  10.0.3.0/24	|   AZ-2
  
👉 Public subnets = Internet-facing

👉 Private subnets = Database layer

