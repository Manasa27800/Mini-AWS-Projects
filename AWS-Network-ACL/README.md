# AWS Network ACL Project

## Project Name
AWS Network ACL Configuration using Public and Private Subnets

---

# Project Description
In this project, I created a VPC with public and private subnets and configured Network ACLs to secure subnet-level traffic.

I created separate Network ACLs for both public and private subnets and configured inbound and outbound rules to allow RDP communication between EC2 instances.

This project demonstrates how Network ACLs act as a subnet-level firewall to control traffic.

---

# Project Reference
This project continues from the previous Bastion Host and NAT Gateway projects.

## Reference Projects
👉[AWS Bastion Host Project]https://github.com/Manasa27800/Mini-AWS-Projects/tree/d7ee1846ef897b79b9648dd229ad13dbc5b3d4c6/AWS-Bastion-Host-Project


# Services Used
- Amazon VPC
- Public Subnet
- Private Subnet
- Route Tables
- Internet Gateway
- Network ACLs
- Amazon EC2
- Security Groups
- Remote Desktop Protocol (RDP)

---

# Step 1: Create VPC
- Created a custom VPC.

---

# Step 2: Create Subnets
- Created:
  - Public Subnet
  - Private Subnet

---

# Step 3: Create Route Tables
- Created:
  - Public Route Table
  - Private Route Table

---

# Step 4: Create Internet Gateway
- Created an Internet Gateway.
- Attached it to the VPC.

---

# Step 5: Configure Public Route
- Added route in Public Route Table:
  - Destination: `0.0.0.0/0`
  - Target: Internet Gateway

---

# Step 6: Create EC2 Instances

## WebServer-01 (Public Server)
- Enabled Auto-assign Public IP.
- Configured Security Group for RDP access.

## WebServer-02 (Private Server)
- Disabled Auto-assign Public IP.
- Launched inside Private Subnet.

---

# Step 7: Create Public Network ACL
- Created a Public Network ACL.
- Associated it with the Public Subnet.
<img width="3840" height="1280" alt="pub-acl" src="https://github.com/user-attachments/assets/6d1b8cbc-bca3-47f0-bbe0-c2bce5ac38fb" />

---

# Step 8: Test RDP Connection
- Tried connecting to WebServer-01 using RDP.
- Connection failed.
<img width="1606" height="844" alt="error01" src="https://github.com/user-attachments/assets/156a232b-7a1b-4d9f-8100-761306abe510" />

## Reason
By default, custom Network ACLs deny all inbound and outbound traffic.

<img width="3840" height="1198" alt="pub-accl-02" src="https://github.com/user-attachments/assets/e8dfe48d-346d-4229-9c5e-4a2169e719ea" />
<img width="3836" height="1194" alt="pub-acl-03" src="https://github.com/user-attachments/assets/45f321e1-d8fd-4ca6-9c88-1ef4f0c7fbf2" />

---

# Step 9: Configure Public Network ACL Rules

## Inbound Rules

### Rule 100
- Type: RDP
- Protocol: TCP
- Port: 3389
- Source: Anywhere (`0.0.0.0/0`)
- Action: Allow

### Rule 110
- Type: Custom TCP
- Port Range: `1024-65535`
- Source: Anywhere (`0.0.0.0/0`)
- Action: Allow
<img width="3840" height="810" alt="pub-inbound" src="https://github.com/user-attachments/assets/1f30ba9f-2c8e-4aab-a8a5-baa4e961a3e9" />
---

# Why We Use Port Range 1024-65535
This port range is used for ephemeral ports (temporary response ports).

When RDP communication happens:
- Port 3389 handles the main RDP request.
- The response traffic uses dynamic high-numbered ports between `1024-65535`.

Without allowing these ports, the return traffic gets blocked and the connection fails.

---

# Outbound Rules

### Rule 100
- Type: RDP
- Protocol: TCP
- Port: 3389
- Destination: Anywhere (`0.0.0.0/0`)
- Action: Allow

### Rule 110
- Type: Custom TCP
- Port Range: `1024-65535`
- Destination: Anywhere (`0.0.0.0/0`)
- Action: Allow
<img width="3840" height="893" alt="pub-outbund" src="https://github.com/user-attachments/assets/50e74478-14f3-4c44-8a83-c8e6316b543f" />
---

# Step 10: Test Connection Again
- Tried connecting again using RDP.
- Successfully connected to WebServer-01.
<img width="1185" height="790" alt="done" src="https://github.com/user-attachments/assets/9994a228-924f-4935-a06b-d0f63d87d8c3" />
---

# Step 11: Create Private Network ACL
- Created a Private Network ACL.
- Associated it with the Private Subnet.
<img width="3840" height="1007" alt="edit-pri" src="https://github.com/user-attachments/assets/ee0e6618-d30d-440e-8f3e-60eb07261f6b" />

<img width="3840" height="1297" alt="pri-acl" src="https://github.com/user-attachments/assets/4f7de5da-43e2-427f-ab8b-8a4c85ea9f82" />

---

# Step 12: Connect to Private Server
- From WebServer-01, opened Remote Desktop Connection.
- Tried connecting to WebServer-02 using private IP.

- Connection failed.
<img width="2324" height="1256" alt="prierror" src="https://github.com/user-attachments/assets/ee839681-2a71-41ec-bf3b-c11521d1c25c" />

## Reason
The Private Network ACL was still denying inbound and outbound traffic.

---

# Step 13: Configure Private Network ACL Rules

## Inbound Rules

### Rule 100
- Type: RDP
- Protocol: TCP
- Port: 3389
- Source: Public Subnet CIDR
- Action: Allow

### Rule 110
- Type: Custom TCP
- Port Range: `1024-65535`
- Source: Public Subnet CIDR
- Action: Allow
<img width="3832" height="815" alt="pri-inbound" src="https://github.com/user-attachments/assets/106c30ee-6052-4d8e-b9f4-d79eaf3e20e2" />


---

# Outbound Rules

### Rule 100
- Type: RDP
- Protocol: TCP
- Port: 3389
- Destination: Public Subnet CIDR
- Action: Allow

### Rule 110
- Type: Custom TCP
- Port Range: `1024-65535`
- Destination: Public Subnet CIDR
- Action: Allow


---

# Step 14: Test Connection Again
- Tried connecting again through the Bastion Host.
- Successfully connected to the private EC2 instance.
<img width="2324" height="1256" alt="prierror" src="https://github.com/user-attachments/assets/ccb8ab86-b552-4ccb-a7f6-546b8cc2c44e" />


---

# What is a Network ACL?
A Network ACL (Access Control List) is a subnet-level firewall in AWS.

It controls:
- Inbound traffic entering the subnet.
- Outbound traffic leaving the subnet.

Network ACLs provide an additional layer of security for subnets.

---

# Project Outcome
- Successfully configured Public and Private Network ACLs.
- Controlled subnet-level traffic using inbound and outbound rules.
- Allowed secure RDP communication between EC2 instances.
- Understood how Network ACLs improve subnet security.

---

# Architecture Flow
Internet → Public Subnet → Bastion Host → Private Subnet → Private EC2

