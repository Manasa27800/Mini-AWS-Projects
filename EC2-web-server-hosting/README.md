# AWS EC2 Apache Web Server Hosting Project

## Project Overview

This project demonstrates how to host a static website on an AWS EC2 Ubuntu instance using Apache Web Server.

---

# Step 1: Launch EC2 Instance

1. Open AWS Console
2. Go to EC2 Dashboard
3. Click **Launch Instance**

## Configuration Used

| Setting | Value |
|---|---|
| AMI | Ubuntu |
| Instance Type | t2.micro |
| Key Pair | Existing Key Pair |
| Security Group | linux-sg |
<img width="3840" height="2012" alt="ec2" src="https://github.com/user-attachments/assets/2cc549b7-4188-4301-a90d-a4043f7497b1" />
<img width="3840" height="2014" alt="ec2_02" src="https://github.com/user-attachments/assets/02ae7ee8-614f-43f2-b5ff-0a2df443a778" />

4. Click **Launch Instance**
<img width="3840" height="2015" alt="ec2_03" src="https://github.com/user-attachments/assets/ebe06e27-5b1c-496a-812c-f954da2882fc" />

---

# Step 2: Connect EC2 Instance using SSH
<img width="3840" height="2012" alt="ec2_04" src="https://github.com/user-attachments/assets/d4dbbd83-6852-4420-9f64-331195d4bb73" />

Open Git Bash and run:

```bash
ssh -i your-key.pem ubuntu@YOUR-PUBLIC-IP
```

Successfully connected to Ubuntu EC2 instance.
<img width="1460" height="1129" alt="ssh" src="https://github.com/user-attachments/assets/c85223d1-6d88-4ddd-ad84-682f865f9e3c" />
<img width="1451" height="1179" alt="ubuntu" src="https://github.com/user-attachments/assets/c188e06a-ba98-4604-84f9-0310e87796d6" />

---

# Step 3: Update Packages

Run:

```bash
sudo apt update
```
<img width="1079" height="122" alt="apt" src="https://github.com/user-attachments/assets/401624f1-5bc8-4201-9451-6514112975ad" />

---

# Step 4: Install Apache Web Server

Run:

```bash
sudo apt install apache2 -y
```
<img width="1438" height="174" alt="apacehe" src="https://github.com/user-attachments/assets/e3035372-ebae-402e-a3ab-91a61d8d47a2" />

---

# Step 5: Start Apache Service

Run:

```bash
sudo systemctl start apache2
```
<img width="1397" height="182" alt="apacehe_02" src="https://github.com/user-attachments/assets/cdc2409f-a74d-415b-9701-aa20e0030a3e" />

Enable Apache service:

```bash
sudo systemctl enable apache2
```
<img width="1446" height="122" alt="apacehe_03" src="https://github.com/user-attachments/assets/09e2feaf-bcc4-4c6e-a00f-bfb28568e631" />

---

# Step 6: Check Apache Default Website

Open browser and enter:

```bash
http://YOUR-PUBLIC-IP
```
<img width="704" height="272" alt="web" src="https://github.com/user-attachments/assets/f74399b4-5b7e-42c6-a398-9e87a3af640a" />
<img width="2854" height="1261" alt="web_02" src="https://github.com/user-attachments/assets/3820c442-4e4a-4d67-9f08-4b5b77240a45" />
<img width="1346" height="216" alt="index" src="https://github.com/user-attachments/assets/5101ce71-1701-4df9-9447-40c4bbfb42ee" />
<img width="1552" height="1324" alt="index_02" src="https://github.com/user-attachments/assets/69dd91c8-48c6-43f9-9bcc-80baa7da8c36" />


Initially website was not accessible even when html default code is present because HTTP traffic was blocked in Security Group.

---

# Step 7: Configure Security Group

1. Open EC2 Dashboard
2. Go to Security Groups
3. Select **linux-sg**
4. Click **Edit Inbound Rules**
5. Add new rule:
<img width="3391" height="871" alt="security" src="https://github.com/user-attachments/assets/342d4691-a8b3-4482-88a7-62763df28a89" />

| Type | Protocol | Port Range | Source |
|---|---|---|---|
| HTTP | TCP | 80 | 0.0.0.0/0 |
<img width="3080" height="487" alt="security_02" src="https://github.com/user-attachments/assets/b69dbfa3-0b69-4f08-a192-287baba23c6a" />
<img width="3535" height="963" alt="Security_03" src="https://github.com/user-attachments/assets/75d64049-940f-4584-9655-631a31155dfc" />

6. Click **Save Rules**

Now Apache default webpage becomes accessible.
<img width="3834" height="2094" alt="apaecheweb" src="https://github.com/user-attachments/assets/023d04b2-471c-40f8-8055-b5f478923a7c" />

---

# Step 8: Move to Apache Web Directory

Run:

```bash
cd /var/www/html
```
<img width="1346" height="216" alt="index" src="https://github.com/user-attachments/assets/5101ce71-1701-4df9-9447-40c4bbfb42ee" />

---

# Step 9: Remove Default Apache Webpage

Run:

```bash
sudo rm -rf index.html
```
<img width="1552" height="143" alt="recreteindex" src="https://github.com/user-attachments/assets/fc9d615e-9d85-4e3f-a1f7-deb6284ab2e3" />
<img width="781" height="520" alt="indexdelete" src="https://github.com/user-attachments/assets/186ea97d-bc50-42cc-986e-61f55e6f164b" />

---

# Step 10: Create New HTML File

Run:

```bash
sudo nano index.html
```

Add your custom HTML website code.
<img width="3840" height="1850" alt="code" src="https://github.com/user-attachments/assets/e4d40cff-6101-4d88-8de9-9919b7aa9f4a" />


---

# Step 11: Save File in Nano

Press:

```bash
CTRL + O
```

Press:

```bash
Enter
```

Exit nano:

```bash
CTRL + X
```

---

# Step 12: Verify Hosted Website

Open browser and enter:

```bash
http://YOUR-PUBLIC-IP
```

Custom hosted webpage is successfully running on Apache Web Server.
<img width="3820" height="1825" alt="wedone" src="https://github.com/user-attachments/assets/7ddef5cf-a1ef-4355-bae0-0c6ee9f51825" />

---

# Services Used

- AWS EC2
- Ubuntu Linux
- Apache Web Server
- Security Groups
- Git Bash

---

# Project Outcome

Successfully hosted a static website on AWS EC2 using Apache Web Server and configured Security Groups for HTTP access.

---

# Author

Manasa
