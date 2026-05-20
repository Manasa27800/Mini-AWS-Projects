# AWS EC2 Windows + EBS Volume Expansion Project

## Project Overview

In this project, I launched a Windows EC2 instance on AWS, connected to it using Remote Desktop Protocol (RDP), created and attached an additional EBS volume, initialized the disk in Windows, and later increased the storage size dynamically without data loss.

This project demonstrates:
- EC2 Windows setup
- RDP connection
- EBS volume creation
- Disk initialization in Windows
- Live storage expansion

---

# Architecture Used

- Amazon EC2
- Amazon EBS
- Windows Server
- Remote Desktop Protocol (RDP)

---

# EC2 Windows RDP Connection

For detailed EC2 Windows setup and RDP connection steps, check my previous project:

👉 https://github.com/Manasa27800/Mini-AWS-Projects.git


# Services Used

- Amazon EC2
- Amazon EBS
- Windows Server
- RDP

---

# Step 1 — Launch Windows EC2 Instance

1. Login to AWS Console
2. Open EC2 Dashboard
3. Click Launch Instance
4. Select:
   - Windows Server AMI
   - Free Tier Eligible Instance
5. Create or Select Key Pair
6. Allow RDP (Port 3389) in Security Group
7. Launch Instance

---

# Step 2 — Connect EC2 Using RDP

1. Select EC2 Instance
2. Click Connect
3. Choose RDP Client
4. Download RDP File
5. Get Administrator Password using Key Pair
6. Open RDP File
7. Login to Windows Server

---

# Step 3 — Create Additional EBS Volume

1. Go to EC2 Dashboard
2. Open Volumes
3. Click Create Volume
4. Configure:
   - Size: 10 GB
   - Same Availability Zone as EC2
   - Volume Type: gp2/gp3
5. Add Name Tag
6. Click Create Volume
<img width="3840" height="2160" alt="creating_volume" src="https://github.com/user-attachments/assets/da0d550b-7b76-4e5b-9738-d9bac0379512" />
<img width="3425" height="808" alt="created_vloume" src="https://github.com/user-attachments/assets/5276f67c-830e-45b2-8e51-032a14bf6ff0" />

---

# Step 4 — Attach Volume to EC2

1. Select Created Volume
2. Click:
```txt
Actions → Attach Volume
```

3. Select EC2 Instance
4. Attach Volume
<img width="3840" height="2160" alt="attach" src="https://github.com/user-attachments/assets/a4ccc04e-eae9-4312-a9be-47acb6269431" />
<img width="3840" height="2160" alt="attach_02" src="https://github.com/user-attachments/assets/5cf86c8f-2e1c-4e18-b2c6-ee8b3f7446e3" />

---

# Step 5 — Initialize Disk in Windows

Inside Windows EC2:

1. Press:
```txt
Windows + R
```

2. Type:
```txt
diskmgmt.msc
```
<img width="868" height="603" alt="windowsR" src="https://github.com/user-attachments/assets/70204dfc-5bc2-4a1f-b7d2-809eac902f63" />

3. Disk Management Opens

4. New Disk Appears:
   - Offline
   - Unallocated
<img width="3840" height="2160" alt="offline" src="https://github.com/user-attachments/assets/6f79c9e4-6123-40ac-a8a1-f4c08d2862db" />

5. Right Click Disk:
   - Bring Online
   - Initialize Disk
 <img width="570" height="681" alt="initilaze" src="https://github.com/user-attachments/assets/e5d605bf-7f6e-4e5d-8f45-9593b5e91987" />    
<img width="3840" height="2160" alt="online" src="https://github.com/user-attachments/assets/4ed1fdb3-6b61-4929-90a5-c3f3bcf3a866" />
<img width="1884" height="1110" alt="thispc" src="https://github.com/user-attachments/assets/e2d24349-9308-445a-ab03-9e5e664ad61c" />

6. Create New Simple Volume
<img width="1153" height="746" alt="newvolume" src="https://github.com/user-attachments/assets/74a21e85-c4ae-4e11-a440-3eab488b3c75" />

7. Assign Drive Letter

8. Format Disk:
   - NTFS
   - Quick Format

9. Give Volume Name
<img width="1008" height="931" alt="givename" src="https://github.com/user-attachments/assets/9e5d7d15-8048-4a30-a099-0e4ee80fccc9" />
<img width="939" height="931" alt="diskvolume" src="https://github.com/user-attachments/assets/d4906e50-83a0-4e65-8143-cfd5514df2c6" />



10. Finish Setup
<img width="961" height="1021" alt="newvolume_02" src="https://github.com/user-attachments/assets/974093a7-e589-4fa3-bd79-1bafebf4b6f8" />
---

# Step 6 — Verify New Storage

1. Open:
```txt
This PC
```


2. Newly Created Drive Appears with 10 GB Storage
<img width="1845" height="1203" alt="thispc2" src="https://github.com/user-attachments/assets/d49f7bac-da71-4e6f-9834-c6b0c657da8c" />
---

# Step 7 — Modify EBS Volume Size

1. Go Back to AWS Console
2. Open Volumes
3. Select Attached Volume
4. Click:
```txt
Actions → Modify Volume
```
<img width="3416" height="1051" alt="modify" src="https://github.com/user-attachments/assets/bb572e4e-5a06-4fa8-9665-88c46d532fb0" />

5. Increase Storage Size:
```txt
10 GB → 15 GB
```
<img width="3498" height="1332" alt="modify_02" src="https://github.com/user-attachments/assets/fe82d592-ad04-4c10-901c-557653cb70f6" />

6. Save Changes

---

# Step 8 — Extend Volume in Windows

Inside Windows Server:

1. Open:
```txt
diskmgmt.msc
```

2. Click:
```txt
Action → Refresh
```
<img width="1333" height="1016" alt="refresh" src="https://github.com/user-attachments/assets/13492be6-4193-4d38-bc22-456c6bb0a507" />

3. Additional Unallocated Storage Appears
<img width="3840" height="2160" alt="modiftyed" src="https://github.com/user-attachments/assets/585083b4-bc1d-49e9-b88e-88a39fc8be08" />

4. Right Click Existing Volume

5. Select:
```txt
Extend Volume
```
<img width="1787" height="946" alt="extentede" src="https://github.com/user-attachments/assets/ace50d65-66be-42d1-9f89-42b1f23a7c68" />

6. Complete Extension Wizard

---

# Step 9 — Verify Extended Storage
<img width="3840" height="2160" alt="exdone" src="https://github.com/user-attachments/assets/5469d0a6-252f-4910-9217-6fd27936e4d7" />

1. Open:
```txt
This PC
```

2. Storage Size Now Shows Increased Capacity
<img width="2173" height="1206" alt="thispc3" src="https://github.com/user-attachments/assets/9cf9804c-f984-474c-883d-cf8045218c55" />



# Key Concepts Learned

- Amazon EC2
- Amazon EBS
- Windows Server
- RDP Connection
- Disk Management
- Volume Expansion
- Cloud Storage Scaling

---

# Conclusion

Successfully launched a Windows EC2 instance, connected using RDP, created and attached an EBS volume, initialized and formatted the disk in Windows Server, and later expanded the storage dynamically without data loss.
