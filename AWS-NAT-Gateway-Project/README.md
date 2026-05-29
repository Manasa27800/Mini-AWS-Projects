# AWS NAT Gateway Project

## Project Name
AWS NAT Gateway Setup using Public and Private Subnets

---

# Project Description
In this project, I created a VPC with public and private subnets and configured a NAT Gateway to provide internet access to private EC2 instances.

The public EC2 instance was used as a Bastion Host to connect to the private EC2 instance using RDP.

Initially, the private server did not have internet access. After configuring the NAT Gateway and updating the Route Table, the private server successfully accessed the internet.

---

# Project Reference
This project continues from the previous Bastion Host setup project.

## Reference Project
👉 [Add your Bastion Host GitHub project link here]https://github.com/Manasa27800/Mini-AWS-Projects/tree/9812abeaaa943e0018fd95b78d4664d74a9e81c6/AWS-Bastion-Host-Project

---

# Services Used
- Amazon VPC
- Public Subnet
- Private Subnet
- Internet Gateway
- NAT Gateway
- Route Tables
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

# Step 3: Create Internet Gateway
- Created an Internet Gateway.
- Attached it to the VPC.

---

# Step 4: Create Route Tables
- Created:
  - Public Route Table
  - Private Route Table

---

# Step 5: Associate Subnets
- Associated Public Subnet with Public Route Table.
- Associated Private Subnet with Private Route Table.

---

# Step 6: Configure Public Route
- Edited the Public Route Table.
- Added:
  - Destination: `0.0.0.0/0`
  - Target: Internet Gateway

This allowed internet access for public resources.

---

# Step 7: Create EC2 Instances

## WebServer-01 (Public Server)
- Enabled Auto-assign Public IP.
- Configured Security Group for RDP access.

## WebServer-02 (Private Server)
- Disabled Auto-assign Public IP.
- Launched inside the Private Subnet.

---

# Step 8: Connect to Public Server
- Connected to WebServer-01 using RDP.

## Internet Test
- Opened Microsoft Edge.
- Searched `google.com`.
- Website opened successfully.
<img width="3441" height="1601" alt="pubgoogle" src="https://github.com/user-attachments/assets/09814f45-ce6c-45ba-bccf-8dab92f94812" />

## CMD Test
- Opened Command Prompt.
- Ran:
```cmd
ping google.com
```
<img width="1443" height="884" alt="pubcmd" src="https://github.com/user-attachments/assets/ce9520e2-8b2c-4a11-87b2-7deebe923318" />

- Replies were received successfully.

This confirmed that the public server had internet access.

---

# Step 9: Connect to Private Server
- From WebServer-01, opened Remote Desktop Connection using `Windows + R`.
- Connected to WebServer-02 using the private IP address.

---

# Step 10: Test Internet in Private Server

## Microsoft Edge Test
- Tried opening `google.com`.
- Internet did not work.

## CMD Test
- Ran:
```cmd
ping google.com
```
<img width="1443" height="800" alt="pricmd2" src="https://github.com/user-attachments/assets/021d2ff7-9d72-4703-8f16-65ac281c3298" />


- Request timed out.

This happened because the private server did not have internet access.

---

# Step 11: Create NAT Gateway
- Created a NAT Gateway inside the Public Subnet.
- Allocated an Elastic IP address.
<img width="3836" height="1947" alt="nat_01" src="https://github.com/user-attachments/assets/e7bc4286-b090-4cd3-b7d4-44c929e7a3f0" />

---

# Step 12: Configure Private Route Table
- Edited the Private Route Table.
- Added:
  - Destination: `0.0.0.0/0`
  - Target: NAT Gateway
<img width="3832" height="900" alt="nat_02" src="https://github.com/user-attachments/assets/f208a1c1-3444-48ad-8810-4583d5533e76" />
<img width="3824" height="503" alt="nat_03" src="https://github.com/user-attachments/assets/7bc0cd10-b77d-450d-aa1f-da3edd72812b" />

---

# Step 13: Test Internet Again

## CMD Test
- Ran:
```cmd
ping google.com
```
<img width="1477" height="770" alt="pricmd" src="https://github.com/user-attachments/assets/021d72b5-4a8f-479f-a4ec-66f7011ede2c" />


- Replies were received successfully.

## Browser Test
- Opened Microsoft Edge.
- Searched `google.com`.
- Internet worked successfully.
<img width="3301" height="1672" alt="prigoogle" src="https://github.com/user-attachments/assets/7c49ff75-7d4c-4a12-8ea8-9dca0f238d66" />

This confirmed that the private EC2 instance was accessing the internet through the NAT Gateway.

---

# Project Outcome
- Successfully configured NAT Gateway.
- Enabled internet access for private EC2 instance.
- Verified internet connectivity using browser and CMD.
- Successfully implemented Bastion Host and NAT Gateway architecture.

---

# Architecture Flow
Internet → Internet Gateway → Public EC2 / NAT Gateway → Private EC2

