# AWS Auto Scaling Web Server Deployment using EC2, Launch Template, CloudWatch, SNS & Step Scaling

## 📌 Project Overview

This project demonstrates how to build a highly available and automatically scalable web application on AWS using **Amazon EC2 Auto Scaling**.

The project starts by creating a custom VPC with a public subnet, deploying an Apache web server on Ubuntu, hosting a custom website, creating an Amazon Machine Image (AMI), configuring a Launch Template, and implementing Dynamic Auto Scaling using CloudWatch alarms, Step Scaling Policies, and Amazon SNS email notifications.

The Auto Scaling Group automatically launches new EC2 instances during high CPU utilization and terminates unnecessary instances when traffic decreases, ensuring high availability while optimizing infrastructure costs.

---

# 🏗️ Architecture

```
                    Internet
                        │
                Internet Gateway
                        │
                  Route Table
                        │
                 Public Subnet
                        │
               Auto Scaling Group
                        │
               Launch Template
                        │
              Ubuntu EC2 Instances
                        │
              Apache Web Server
                        │
                Hosted Website

CloudWatch
     │
     ├── High CPU Alarm
     │        │
     │        ├── SNS Email Notification
     │        └── Scale-Out Policy
     │
     └── Low CPU Alarm
              │
              └── Scale-In Policy
```

---

# 🛠️ AWS Services Used

- Amazon VPC
- Public Subnet
- Route Table
- Internet Gateway
- Security Group
- Amazon EC2
- Ubuntu Server
- Apache2 Web Server
- Amazon Machine Image (AMI)
- Launch Template
- Auto Scaling Group
- Amazon CloudWatch
- Amazon SNS
- IAM
- Linux Stress Tool

---

# 🚀 Project Workflow

## Step 1: Create a Custom VPC

Created a custom Amazon VPC to isolate the networking resources.

### Configuration

- Custom CIDR Block
- DNS Resolution Enabled
- DNS Hostnames Enabled

### Purpose

The VPC provides a secure virtual network where all AWS resources communicate with each other.

---

## Step 2: Create a Public Subnet

Created a public subnet inside the VPC.

### Purpose

The public subnet allows EC2 instances to access the Internet.

---

## Step 3: Create and Attach Internet Gateway

Created an Internet Gateway and attached it to the VPC.

### Purpose

Provides Internet connectivity to resources inside the VPC.

---

## Step 4: Configure Route Table

Created a Route Table with the following route.

```
Destination : 0.0.0.0/0

Target : Internet Gateway
```

Associated the Route Table with the Public Subnet.

### Purpose

Allows all outbound Internet traffic through the Internet Gateway.

---

## Step 5: Launch Ubuntu EC2 Instance

Launched an Ubuntu EC2 instance inside the Public Subnet.

### Security Group Configuration

| Type | Port | Source |
|------|------|---------|
| SSH | 22 | My IP |
| HTTP | 80 | Anywhere (0.0.0.0/0) |

### Purpose

- SSH is used for remote administration.
- HTTP allows users to access the hosted website.

---

## Step 6: Connect to EC2

Connected to the EC2 instance using SSH.

```bash
ssh -i key.pem ubuntu@Public-IP
```

Switch to root user.

```bash
sudo -i
```

---

## Step 7: Install Apache Web Server

Update packages.

```bash
apt update
```

Install Apache.

```bash
apt install apache2 -y
```

Enable Apache.

```bash
systemctl enable apache2
```

Start Apache.

```bash
systemctl start apache2
```

Verify installation.

```bash
systemctl status apache2
```

---

## Step 8: Verify Apache Installation

Opened the EC2 Public IP in the browser.

```
http://Public-IP
```

The default Apache webpage appeared successfully.

This confirms that Apache was installed correctly.

---

## Step 9: Host Custom Website

Removed the default Apache webpage.

```bash
rm /var/www/html/index.html
```

Created a new webpage.

```bash
nano /var/www/html/index.html
```

Added custom HTML and CSS code.

Saved the file and refreshed the browser.
<img width="1589" height="1111" alt="index" src="https://github.com/user-attachments/assets/b8f73760-f781-473a-993a-553b1be191ae" />

The custom website was successfully hosted.
<img width="3840" height="1794" alt="web" src="https://github.com/user-attachments/assets/73cb3e82-5bd7-4eee-b376-e8c540181b90" />

---

## Step 10: Create Amazon Machine Image (AMI)

Created a custom Amazon Machine Image after configuring the web server.
<img width="3840" height="1944" alt="creating ami " src="https://github.com/user-attachments/assets/97bbed6f-4794-4403-a8e6-d29b6a4ec042" />
<img width="3840" height="648" alt="ami" src="https://github.com/user-attachments/assets/0cfc5124-942e-48c5-a9c4-3bfa31725a53" />

### Why use an AMI?

The AMI stores:

- Ubuntu Operating System
- Apache Installation
- Website Files
- Server Configuration

Whenever Auto Scaling launches a new EC2 instance, it uses this AMI so every server is configured identically.

---

## Step 11: Create Launch Template

Created a Launch Template using the custom AMI.
<img width="3840" height="1950" alt="tem1" src="https://github.com/user-attachments/assets/c801c951-a53d-43b1-9931-b2c511e77de8" />
<img width="3840" height="1887" alt="tem2" src="https://github.com/user-attachments/assets/c5d6ec52-f680-48d0-b134-29d893c27359" />

### Configuration

- Custom AMI
- Instance Type
- Security Group
- Key Pair
- Storage Configuration

### Purpose

A Launch Template acts as a reusable blueprint for launching EC2 instances.

Instead of configuring every new server manually, Auto Scaling uses the Launch Template to create identical instances automatically.

---

## Step 12: Create Auto Scaling Group

Created an Auto Scaling Group using the Launch Template.
<img width="3816" height="1891" alt="auto1" src="https://github.com/user-attachments/assets/b97c1bb0-5cb6-45a6-bb66-4e73e751b2be" />
<img width="3840" height="1888" alt="auto2" src="https://github.com/user-attachments/assets/5d122c44-e1a1-4ba6-b23a-fd0b92102d8a" />
<img width="3834" height="683" alt="autoec2" src="https://github.com/user-attachments/assets/e12429ca-b724-4bc0-98e8-45b5a14adfd4" />

### Capacity Configuration

| Setting | Value |
|----------|-------|
| Minimum Capacity | 1 |
| Desired Capacity | 1 |
| Maximum Capacity | 3 |

Initially, one EC2 instance was running.

The Auto Scaling Group manages the lifecycle of EC2 instances automatically.

---

# 📈 Understanding Auto Scaling

Amazon EC2 Auto Scaling automatically adjusts the number of EC2 instances based on application demand.

### Benefits

- High Availability
- Fault Tolerance
- Automatic Recovery
- Cost Optimization
- Improved Performance
- Reduced Manual Administration

Without Auto Scaling, one server can become overloaded during high traffic.

With Auto Scaling enabled, additional servers are automatically launched to handle increased demand.

When traffic decreases, unnecessary servers are automatically terminated, reducing AWS costs.

---

# ⚡ Auto Scaling Methods

AWS provides multiple scaling methods.

## 1. Manual Scaling

The administrator manually changes the desired number of EC2 instances.

Example:

- Increase from 2 to 5 instances manually.

Suitable only for testing or maintenance.

---

## 2. Scheduled Scaling

Automatically scales resources at predefined times.

Example:

- Increase servers every weekday at 9 AM.
- Reduce servers every night at 10 PM.

Best for predictable workloads.

---

## 3. Dynamic Scaling

Automatically adjusts capacity based on CloudWatch metrics.

Common metrics include:

- CPU Utilization
- Network Traffic
- Request Count
- Custom Metrics

No manual intervention is required.

---

## 4. Target Tracking Scaling

AWS automatically maintains a target metric.

Example:

Maintain average CPU utilization at **50%**.

AWS automatically launches or terminates EC2 instances to maintain the target.

This is the simplest scaling method.

---

## 5. Step Scaling (Used in this Project)

This project uses **Step Scaling**.

Instead of maintaining a target CPU percentage, Step Scaling performs different actions depending on CPU thresholds.

Example:

| CPU Utilization | Action |
|-----------------|--------|
| Above 70% | Add 2 Instances |
| Above 90% | Add 3 Instances |
| Below 30% | Remove 2 Instances |

Step Scaling provides greater control over infrastructure scaling.

---

# 📧 Step 13: Configure Amazon SNS

Created an Amazon SNS Topic.

Subscribed using an email address.

Confirmed the subscription from the received email.

### Purpose

Whenever a CloudWatch alarm changes state, SNS automatically sends an email notification.

Example:

```
CloudWatch Alarm State Change

CPU Utilization exceeded 70%
```

---

# 📊 Step 14: Configure High CPU CloudWatch Alarm

Created a CloudWatch Alarm.
<img width="3840" height="1264" alt="cloud1" src="https://github.com/user-attachments/assets/8eabfe76-debb-48fd-9715-2e0f12b69a45" />
<img width="3623" height="1765" alt="cloud2" src="https://github.com/user-attachments/assets/78531e4e-f8cc-44dc-b5ef-6d6ed0193ce7" />
<img width="3813" height="1716" alt="cloud3" src="https://github.com/user-attachments/assets/7edce15f-4138-43be-98e9-a3f1aecf7233" />
<img width="3840" height="1702" alt="cloud4" src="https://github.com/user-attachments/assets/cd5d494c-de56-4ccb-8db5-3298de06386e" />

### Configuration

Metric

```
CPU Utilization
```

Threshold

```
Greater than 70%
```

Evaluation Period

```
1 Consecutive Period
```

Actions

- Send SNS Email Notification
- Trigger Scale-Out Policy

---

# 📈 Step 15: Configure Step Scaling (Scale Out)
<img width="3840" height="1270" alt="dyanmic" src="https://github.com/user-attachments/assets/84feb0d5-235a-4506-b93f-165e533ed245" />
<img width="3296" height="1573" alt="dynamic2" src="https://github.com/user-attachments/assets/76bdf3cf-8c41-427b-a849-8c38bb1d2d61" />

Created a Dynamic Step Scaling Policy.

### Policy

```
CPU > 70%

Add 2 EC2 Instances
```

Maximum Capacity

```
3 Instances
```

When CPU utilization exceeded 70%, Auto Scaling automatically launched two additional EC2 instances.

---

# 🔥 Step 16: Generate CPU Load

Installed the Stress tool.
<img width="964" height="208" alt="stress1" src="https://github.com/user-attachments/assets/d94d526d-a3ba-4b6e-9d9c-754c998d5240" />

```bash
apt install stress -y
```

Generated CPU load.
<img width="1557" height="135" alt="stress2" src="https://github.com/user-attachments/assets/c4dc8888-b8cc-47bb-91c7-d6b4e2412481" />

```bash
stress --cpu 4 --timeout 300
```

### Observations
<img width="3655" height="1389" alt="cpu moin" src="https://github.com/user-attachments/assets/c3496808-750f-48b5-b87a-6bed281e8867" />
<img width="3326" height="579" alt="warmimg1" src="https://github.com/user-attachments/assets/6bbf7b9d-de53-4dae-ae06-3307208abd53" />
<img width="3167" height="634" alt="warning2" src="https://github.com/user-attachments/assets/f35f5d91-5f2d-4e79-8a90-abc720cd390f" />
<img width="3111" height="1467" alt="newinstances" src="https://github.com/user-attachments/assets/054b880a-6c55-4df7-832a-f2e7e733db59" />
<img width="3415" height="659" alt="ec2newinstances" src="https://github.com/user-attachments/assets/9e139d19-a01e-4560-9352-020fcdaebaa1" />


- CPU utilization increased.
- CloudWatch Alarm changed from **OK** to **ALARM**.
- SNS sent an email notification.
- Auto Scaling Group launched additional EC2 instances.
- Total running instances increased from **1 → 3**.

This verified that Scale-Out was working successfully.

---

# 📉 Step 17: Configure Scale-In Policy

Created another Dynamic Step Scaling Policy.
<img width="2727" height="1803" alt="cloudlower" src="https://github.com/user-attachments/assets/246571aa-0cda-4ad2-88c0-bc576657c471" />
<img width="3224" height="712" alt="cloud6" src="https://github.com/user-attachments/assets/bfe2bad5-9e69-4f5a-bc95-8f14908c2870" />
<img width="3157" height="1222" alt="terminated" src="https://github.com/user-attachments/assets/c3d163ef-37c6-475b-94bb-22f40853c531" />
<img width="3394" height="633" alt="ec2down" src="https://github.com/user-attachments/assets/04046d6e-d952-4949-96a9-c760c1406038" />

Created a second CloudWatch Alarm.

### Configuration

Metric

```
CPU Utilization
```

Threshold

```
Below 30%
```

Action

```
Terminate 2 EC2 Instances
```

### Purpose

When application traffic decreases, unnecessary EC2 instances are automatically removed to reduce infrastructure costs.

---

# 📉 Step 18: Verify Scale-In

Stopped the Stress process.

CPU utilization gradually decreased.

### Observations

- CloudWatch Alarm changed from **ALARM** to **OK**.
- Scale-In Policy was triggered.
- Auto Scaling Group terminated unnecessary EC2 instances.
- Running instances reduced from **3 → 1**.

This confirmed that automatic Scale-In was functioning correctly.

---

# ✅ Project Outcome

Successfully deployed a highly available and automatically scalable web application on AWS.

Implemented:

- Custom VPC Networking
- Apache Web Server Deployment
- Static Website Hosting
- Custom Amazon Machine Image
- Launch Template
- Auto Scaling Group
- Dynamic Step Scaling
- CloudWatch Monitoring
- CloudWatch Alarms
- Amazon SNS Notifications
- Automatic Scale-Out
- Automatic Scale-In
- CPU Load Testing using Linux Stress Tool

The infrastructure automatically scaled up during high CPU utilization and scaled down after the workload decreased, demonstrating an efficient and production-like AWS Auto Scaling implementation.

---

# 📚 Key Learning Outcomes

- Amazon VPC Networking
- Public Subnets
- Route Tables
- Internet Gateway
- EC2 Deployment
- Linux Administration
- Apache Web Server
- Static Website Hosting
- Security Groups
- Amazon Machine Image (AMI)
- Launch Templates
- Auto Scaling Groups
- CloudWatch Metrics
- CloudWatch Alarms
- Amazon SNS
- Dynamic Step Scaling
- High Availability
- Cost Optimization
- Infrastructure Automation
- Performance Monitoring
- CPU Stress Testing
