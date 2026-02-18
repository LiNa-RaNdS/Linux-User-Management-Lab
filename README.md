# **Linux User Management Lab – Kali Linux**

## **Lab Title**

Linux User Management and File Permission Configuration

## **Objective**

The objective of this lab is to demonstrate hands-on knowledge of Linux user and group management, file ownership, and permission control. The lab simulates a real-world organizational environment by configuring secure access for two departments Marketing and IT using Kali Linux.

## **Tools Used**

* **OS:** Kali Linux  
* **Terminal:** Linux Bash shell  
* **Commands:**  
  * adduser / useradd  
  * groupadd  
  * usermod  
  * chown  
  * chmod  
* **Platform:** GitHub for documentation and version control

## **Scenario Overview**

TechCorp Solutions requires proper access control for departmental resources:

* **Marketing Department**  
  * Each employee must have a private file.  
  * No other users or groups should access these files.  
* **IT Department**  
  * All IT employees must collaborate on one shared file.  
  * Only IT members should have access.
---
## **Step-by-Step Process**

### **1\. Shared Directory Creation**

Two shared directories were created to store departmental files:

* /home/shared/marketing  
* /home/shared/itdept
```bash
sudo mkdir \-p /home/shared/marketing  
sudo mkdir \-p /home/shared/itdept
```
### **2\. Marketing Department Configuration**

#### **2.1 Group Creation**

A group named marketing was created to represent the Marketing department.

```bash
sudo groupadd marketing
```

#### **2.2 User Creation**

Five users were created for the Marketing department:

* alice_m  
* bob_m  
* carol_m  
* david_m  
* emma_m

```bash
sudo adduser alice_m 
sudo adduser bob_m  
sudo adduser carol_m  
sudo adduser david_m  
sudo adduser emma_m
```
#### **2.3 Adding Users to the Marketing Group**
```
sudo usermod -aG marketing alice_m
sudo usermod -aG marketing bob_m
sudo usermod -aG marketing carol_m
sudo usermod -aG marketing david_m
sudo usermod -aG marketing emma_m
```
#### **2.4 Individual File Creation**

Each Marketing user was assigned a personal file in the shared directory:
```
touch /home/shared/marketing/alice_report.txt
touch /home/shared/marketing/bob_report.txt
touch /home/shared/marketing/carol_report.txt
touch /home/shared/marketing/david_report.txt
touch /home/shared/marketing/emma_report.txt
```
#### **2.5 File Ownership Assignment**

Each file was owned by its corresponding user to ensure individual accountability.
```
sudo chown alice_m:marketing /home/shared/marketing/alice_report.txt
sudo chown bob_m:marketing /home/shared/marketing/bob_report.txt
sudo chown carol_m:marketing /home/shared/marketing/carol_report.txt
sudo chown david_m:marketing /home/shared/marketing/david_report.txt
sudo chown emma_m:marketing /home/shared/marketing/emma_report.txt
```
#### **2.6 Permission Configuration**

Permissions were set to **700** to ensure full privacy (Owner access only).
```
sudo chmod 700 /home/shared/marketing/*.txt
```
**Permission Breakdown:**

* **Owner:** read, write, execute (7)  
* **Group:** no access (0)  
* **Others:** no access (0)
---

### **3\. IT Department Configuration**

#### **3.1 Group Creation**

An IT department group named itdept was created.
```
sudo groupadd itdept
```
#### **3.2 User Creation**

Five IT users were created:

* frank_it  
* grace_it  
* henry_it  
* iris_it  
* jack_it
```
sudo adduser frank_it
sudo adduser grace_it
sudo adduser henry_it
sudo adduser iris_it
sudo adduser jack_it
```
#### **3.3 Adding Users to the IT Group**
```
sudo usermod -aG itdept frank_it
sudo usermod -aG itdept grace_it
sudo usermod -aG itdept henry_it
sudo usermod -aG itdept iris_it
sudo usermod -aG itdept jack_it
```
#### **3.4 Shared File Creation**

A single shared file was created for IT collaboration:
```
touch /home/shared/itdept/project_specs.txt
```
#### **3.5 Ownership and Permissions**

The file was assigned to the itdept group and permissions were set to allow collaborative access (**770**).
```
sudo chown root:itdept /home/shared/itdept/project_specs.txt
sudo chmod 770 /home/shared/itdept/project_specs.txt
```
**Permission Breakdown:**

* **Owner (root):** full access  
* **IT Group (itdept):** full access (read, write, execute)  
* **Others:** no access

## **Verification and Validation**

The following commands were used to verify the correct configuration of users, groups, and permissions:

\# Check all created users  
```
cat /etc/passwd
```
\# Verify group memberships  
```
getent group marketing  
getent group itdept
```
\# Verify file ownership and permission strings  
```
ls -l /home/shared/marketing  
ls -l /home/shared/itdept
```

**Note:** Screenshots of these command outputs are stored in the screenshots/ directory of this repository.
