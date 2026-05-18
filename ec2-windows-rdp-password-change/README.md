# AWS EC2 Windows RDP Password Management Project


## Project Overview

This project demonstrates how to launch a Windows EC2 instance on AWS, connect to it using Remote Desktop Protocol (RDP), retrieve the automatically generated Administrator password using a PEM key pair, and later change the Administrator password manually through Windows Computer Management for easier future access.

This mini project helped me understand practical AWS EC2 management, Windows administration basics, remote access configuration, and password management inside cloud instances.

---

# Architecture / Workflow

AWS Console → Launch Windows EC2 → Generate Key Pair → Retrieve Password → Connect via RDP → Change Administrator Password → Reconnect Using Custom Password

---

# AWS Services Used

- Amazon EC2
- Security Groups
- Key Pairs
- Windows Server
- Remote Desktop Protocol (RDP)

---

# Tools Used

- AWS Management Console
- Remote Desktop Connection
- Windows Computer Management (`compmgmt.msc`)

---

# Step-by-Step Implementation

---

## Step 1 — Launching Windows EC2 Instanc
- Logged into AWS Console
- Navigated to EC2 Dashboard
- Clicked on Launch Instance
<img width="3840" height="2160" alt="launching-ec2" src="https://github.com/user-attachments/assets/211b44e5-afb7-4960-a609-c557a3dee79b" />
- Selected Windows Server AMI
- Selected instance type
- Created and downloaded PEM key pair
  <img width="3840" height="2160" alt="key_pair" src="https://github.com/user-attachments/assets/e991b547-996c-4c61-a7b4-4a5b34249372" />
- Configured security group to allow RDP access on port 3389
  <img width="3840" height="2160" alt="network_setting" src="https://github.com/user-attachments/assets/7db3c287-2ebf-4e00-8dff-479bd389c907" />
- Launched the instance successfully
- 

### Screenshot
<img width="3840" height="2160" alt="Running_server" src="https://github.com/user-attachments/assets/1fe64909-05fb-4d98-8ff9-ecf7ef002f0e" />
## Step 2 — Checking EC2 Instance Status

- Waited for instance status checks to pass
- Verified that the instance was running successfully

## Step 3 — Downloading RDP File

- Selected the Windows EC2 instance
- Clicked Connect
- Downloaded Remote Desktop File
<img width="3840" height="2160" alt="server_rdp" src="https://github.com/user-attachments/assets/b8632125-e704-4dc4-9906-807f8a4bfae4" />

## Step 4 — Retrieving Administrator Password

- Clicked “Get Windows Password” have to wait for 4 minutes
- <img width="3840" height="2160" alt="generating_password" src="https://github.com/user-attachments/assets/a633746d-94fa-43ae-aaba-d3cd4f790ce4" />

- Uploaded PEM key pair file
  <img width="3840" height="2160" alt="generating_password_02" src="https://github.com/user-attachments/assets/17f81645-d01c-4b9c-9040-a57dcf2398d4" />
<img width="3840" height="2160" alt="generating_password_03" src="https://github.com/user-attachments/assets/d35f1ae0-bdab-432f-b35f-4990d9a24743" />

- Decrypted the generated Administrator password

### Screenshot
[Get Password]<img width="3840" height="2160" alt="generating_password_04" src="https://github.com/user-attachments/assets/fe35ab3c-beda-4d8d-91d1-778f95eda243" />


---

## Step 5 — Connecting Using RDP

- Opened Remote Desktop Connection
- Entered public IP / DNS
<img width="3840" height="2160" alt="connecting_rdp" src="https://github.com/user-attachments/assets/6e5a49ea-bf1e-48eb-8223-06c0ef8f24d9" />


- Logged in using Administrator username and decrypted password
- <img width="3840" height="2160" alt="connecting_rdp_02" src="https://github.com/user-attachments/assets/86d687ed-291b-4c48-ac16-cb5c8536590c" />
<img width="3840" height="2160" alt="connecting_rdp_03" src="https://github.com/user-attachments/assets/e6a17900-35e3-4df9-9341-8ca87e2476d7" />

- Successfully connected to Windows Server

### Screenshot
<img width="3840" height="2160" alt="connecting_rdp_04" src="https://github.com/user-attachments/assets/3417e1f7-566d-4d19-98bd-3bb415e2ee83" />




## Step 6 — Opening Computer Management

Inside the Windows Server:

- Opened Run dialog using:
Windows + R
<img width="3840" height="2160" alt="command" src="https://github.com/user-attachments/assets/d4381258-d910-4903-9420-5906c6b203a8" />
Opened Computer Management successfully

## Step 7 — Changing Administrator Password

<img width="3840" height="2160" alt="computer_management" src="https://github.com/user-attachments/assets/59953c31-6ef8-4828-a86c-888ea61d1312" />

Navigated to:
Computer Management > Local Users and Groups > Users
Right-clicked on Administrator user
<img width="3840" height="2160" alt="computer_management_03" src="https://github.com/user-attachments/assets/0c98bf81-ab22-4cee-9cc2-90bbda6ae5ed" />

Selected “Set Password”
<img width="3840" height="2160" alt="computer_management_04" src="https://github.com/user-attachments/assets/331468db-cb71-4c97-9734-1fd3b1af31ec" />

Created custom password
<img width="3840" height="2160" alt="computer_management_05" src="https://github.com/user-attachments/assets/50999113-cc9e-4969-adc9-1127daed9128" />

## Step 8 — Testing New Password

Closed current RDP session
<img width="3840" height="2160" alt="sign_out" src="https://github.com/user-attachments/assets/eb520113-4b62-46c4-9ae7-baa0cf43e281" />

Reconnected again using custom password
Verified successful login
Screenshot
<img width="3840" height="2160" alt="connecting_rdp_04" src="https://github.com/user-attachments/assets/29a49003-8379-4808-b5e1-d853c7ca37da" />

Key Concepts Learned
- Launching Windows EC2 instances
- EC2 instance configuration
- Security Group basics
- RDP remote connection
- PEM key pair usage
- Windows password decryption
- Windows user administration
- Changing Administrator password
- Remote server access management

Challenges Faced
- Understanding how Windows password decryption works
- Connecting through RDP initially
- Learning Windows Computer Management navigation

Outcome

Successfully launched and configured a Windows EC2 instance on AWS, connected remotely using RDP, changed the Administrator password manually, and verified login using the new custom credentials.
