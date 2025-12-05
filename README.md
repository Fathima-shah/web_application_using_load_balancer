# **Highly Available Web Application Using Azure Load Balancer**

This project demonstrates hosting a web application on two Windows Server Virtual Machines running IIS, placed inside an Availability Set, and load balanced using a Public Azure Load Balancer to achieve high availability and fault tolerance.

---

## **1. Provisioned Virtual Network & Resource Group**

- Created a new **Resource Group (`rg`)**
- Created a **Virtual Network (`vnet`)**
- Region selected: **US East**
- Default subnet added automatically
- Deployment completed successfully

---

## **2. Created Windows Virtual Machines (VM1 & VM2)**

### **VM1 Configuration**
- Deployed a **Windows Server Virtual Machine** named `vm1`
- Selected **US East** region
- Chose **Availability Set** option
- Created a new availability set: **`USset`**
- Set a custom secure username & password *(not shared for security purposes)*
- Attached VM to `vnet` and default subnet
- Disabled **Boot Diagnostics**
- Deploy completed successfully

### **VM2 Configuration**
- Created the second VM named `vm2`
- Same region: **US East**
- Selected the same availability set: **`USset`**
- Chose the same `vnet` and default subnet
- Disabled **Boot Diagnostics**
- Deployment completed successfully

---

## **3. Installed IIS Web Server on VM1 & VM2**

- Connected to both VMs using **RDP**
- Opened **Server Manager**
- Installed **Web Server (IIS)** role
- Uploaded website files into:
C:\inetpub\wwwroot
- Configured **Inbound Port Rule (HTTP - Port 80)** in Azure’s VM Networking
- Verified IIS webpage access using each VM’s public IP in the browser

---

## **4. Configured Azure Public Load Balancer**

- Created a **Standard Public Load Balancer (`lb`)**
- Configured a **Frontend IP** named `ip` with a new public IP `newip`
- Created a **Backend Pool (`bpl`)**
- Added both virtual machines: `vm1`, `vm2`
- Created a **Health Probe** named `hp` on **TCP Port 80**
- Added a **Load Balancing Rule (`LBrule`)** with:
- Protocol: **TCP**
- Frontend Port: **80**
- Backend Port: **80**
- Health Probe: `hp`
- Saved configuration and deployed

---

##  **Final Output**

- Accessed the web application using the **Load Balancer Public IP**
- The load balancer routed traffic between the two VMs
- Application remained accessible even if one VM is unavailable
- High Availability successfully achieved

---

## **Project Screenshots**

-Virtual Network & VM Provisioning
- Load Balancer Setup & Backend Pool Configuration
- IIS Installation & Website Deployment
- HTTP Port Configuration & Final Web Test

---

# **Skills Gained**

- Azure Load Balancer (Standard Public)
- IIS Web Hosting on Windows Server
- Availability Set & Fault Domain Concepts
- Virtual Machine Management
- Azure Networking & Inbound Rules
- High Availability Architecture Implementation

---

## **Status**
 Project Completed  
 High Availability Achieved using Azure Load Balancer
