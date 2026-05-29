# AWS Bastion Host Project

## Project Name
AWS Bastion Host Setup using Public and Private Subnets

---

## Project Description
In this project, I created a custom VPC with public and private subnets. I configured route tables, internet gateway, and EC2 instances to create a Bastion Host architecture.

The Bastion Host allows secure access to a private EC2 instance through RDP connection.

---

# Services Used
- Amazon VPC
- Public Subnet
- Private Subnet
- Route Tables
- Internet Gateway
- Amazon EC2
- Security Groups
- Remote Desktop Protocol (RDP)

---

# Step 1: Create VPC
- Created a custom VPC.
<img width="3840" height="1959" alt="vpc01" src="https://github.com/user-attachments/assets/5c782d56-0126-444d-a73e-4ffbaa462f8f" />
<img width="3840" height="1385" alt="vpc02" src="https://github.com/user-attachments/assets/d02270d4-9c65-4f2b-9427-78a4c421fe48" />

---

# Step 2: Create Subnets
- Created one Public Subnet.
- <img width="3840" height="1960" alt="publicsub" src="https://github.com/user-attachments/assets/ae3e5918-e37f-49b7-b8cc-2d923b66222f" />

- Created one Private Subnet.
<img width="3840" height="1937" alt="privatesub" src="https://github.com/user-attachments/assets/c0ae48ee-f699-4bd6-8ade-020c97518f03" />

---

# Step 3: Check Resource Map
- Opened the Resource Map.
- The subnets were not connected properly.
<img width="3840" height="1597" alt="vpc03" src="https://github.com/user-attachments/assets/a5d7503d-5c1b-42cd-814c-55187d1c5117" />

---

# Step 4: Create Route Tables
- Created:
  - Public Route Table
  <img width="3840" height="1213" alt="pubrt" src="https://github.com/user-attachments/assets/e2572c42-40f7-4471-bad4-7a079656a35f" />
 
  - Private Route Table
<img width="3840" height="1219" alt="prirt" src="https://github.com/user-attachments/assets/5409fe37-ed7b-4d85-9128-51d2eb194d5a" />

---

# Step 5: Associate Subnets
- Associated Public Subnet with Public Route Table.
  <img width="3840" height="1073" alt="editpubrt" src="https://github.com/user-attachments/assets/4ecd402c-d6a3-419c-a922-bf7a2dcb4301" />

- Associated Private Subnet with Private Route Table.
<img width="3840" height="1099" alt="editprivrt" src="https://github.com/user-attachments/assets/1decdbe7-f3b8-4f37-afa4-f8ca495bcc8a" />

- After subnet association, the Resource Map showed proper connectivity.
<img width="3832" height="1676" alt="vpc04" src="https://github.com/user-attachments/assets/1fe0c0a9-e4a3-4343-a534-0aa0c275714a" />

---

# Step 6: Create and Attach Internet Gateway
- Created an Internet Gateway.
  <img width="3840" height="1085" alt="igtw" src="https://github.com/user-attachments/assets/af245831-d29d-40c4-b675-a2ad6487cd67" />

- Initially, the Internet Gateway was detached.
  <img width="3840" height="918" alt="deatach" src="https://github.com/user-attachments/assets/57f2707b-bcf3-4591-85b2-5f5da3d7a600" />

- Attached the Internet Gateway to the VPC.
<img width="3790" height="903" alt="actions" src="https://github.com/user-attachments/assets/b396d693-180f-4076-9acf-297710104625" />

---

# Step 7: Create EC2 Instances

## WebServer-01 (Public Server)
- Enabled Auto-assign Public IP.
- Configured Security Group for RDP access.
<img width="3840" height="1951" alt="pubec2net" src="https://github.com/user-attachments/assets/4e9cd4d9-196f-4d9c-b360-bdd315789b52" />

## WebServer-02 (Private Server)
- Disabled Auto-assign Public IP.
- Launched inside the Private Subnet.
<img width="3840" height="1951" alt="privec2net" src="https://github.com/user-attachments/assets/c3b9c7df-1105-41e5-92cc-362541c1b545" />

---

# Step 8: Connect using RDP

## First Attempt
- Tried connecting to WebServer-01 using RDP.
- Connection failed because the Internet Gateway route was not added to the Route Table.
<img width="3840" height="822" alt="error" src="https://github.com/user-attachments/assets/1975a3bf-7a11-404a-a128-c8fff34eced3" />

## Solution
- Edited the Public Route Table.
- Added:
  - Destination: `0.0.0.0/0`
  - Target: Internet Gateway
<img width="3840" height="890" alt="editrt" src="https://github.com/user-attachments/assets/a62324d9-f680-41b4-b9e0-affe6d6e7055" />

## Second Attempt
- Tried connecting again using RDP.
- Successfully connected to WebServer-01.

---

# Step 9: Connect to Private Server using Bastion Host
- Opened Remote Desktop Connection using `Windows + R`.
  <img width="3510" height="1965" alt="rdpofpub" src="https://github.com/user-attachments/assets/2f418e20-ac71-41e3-b129-743145929d51" />

- Entered the private IP address of WebServer-02.
- Successfully connected to the private EC2 instance through WebServer-01.
<img width="3482" height="1957" alt="priserver" src="https://github.com/user-attachments/assets/c63c3d65-8c8c-44ba-a90f-772663ab7727" />

This setup is called a Bastion Host Architecture.

---

# Project Outcome
- Successfully configured VPC networking.
- Connected public and private subnets.
- Configured Route Tables and Internet Gateway.
- Successfully accessed the private server through the Bastion Host.

---

# Architecture Flow
Internet → Public EC2 (Bastion Host) → Private EC2 Instance

