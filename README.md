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
