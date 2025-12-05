Deploy a highly available web application in Azure using:
- Two Virtual Machines in an availability set
- Azure Load Balancer for traffic distribution

---

## 🔹 Step 1: Create a Virtual Network

1. Go to **Azure Portal**
2. Search for **Virtual Network**
3. Click **Create**
4. Select/Enter:
   - **Resource Group:** `rg`
   - **VNet Name:** `vnet`
   - **Region:** *US East*
5. Add default **Subnet**
6. Click **Review + Create**
7. Click **Create**

---

## 🔹 Step 2: Create Virtual Machines

### ➤ VM1 Creation
1. Search **Virtual Machine**
2. Click **Create**
3. Select/Enter:
   - **Resource Group:** `rg`
   - **VM Name:** `vm1`
   - **Region:** *US East*
4. Under Availability:
   - Choose **Availability Set**
   - Click **Create new**
   - Name it **USset**
5. Instance Settings:
   - **Username:** `<vm-userername>`
   - **Password:** `<secure-password>`
6. Networking:
   - Select **VNet:** `vnet`
   - Select **Subnet:** *default*
7. **Disable Boot Diagnostics**
8. Click **Review + Create** → **Create**

### ➤ VM2 Creation
📌 Repeat the same steps as VM1 with:
- **VM Name:** `vm2`

---

## 🔹 Step 3: Install Web Server on VM1 & VM2

### ➤ Connect to each VM
1. Go to **VM Overview**
2. Click **Connect > RDP**
3. Download RDP file and login with:
Username: <vm-username>
Password: <secure-password>

markdown
Copy code

### ➤ Install IIS Web Server
1. Open **Server Manager**
2. Click **Add roles and features**
3. Select:
- **Web Server (IIS)**
- Add features → Finish installation

### ➤ Deploy Web Content
1. Open **File Explorer**
2. Go to:
C:\inetpub\wwwroot

markdown
Copy code
3. Upload/paste your web application files.

### ➤ Enable HTTP Traffic in Azure
1. Go to **VM → Networking**
2. Add **Inbound Port Rule**
3. Change **Port** to **HTTP (Port 80)**
4. Save
5. Copy VM Public IP → Check on browser

📌 Repeat these steps for **vm2** also.

---

## 🔹 Step 4: Create Load Balancer

1. Search **Load Balancer**
2. Click **Create**
3. Select/Enter:
- **Resource Group:** `rg`
- **Name:** `lb`
- **SKU:** Standard
- **Type:** Public

### ➤ Add Frontend IP
- Name: `ip`
- Create Public IP:
- Name: `newip`
- Save

### ➤ Create Backend Pool
- Name: `bpl`
- Select **VNet: `vnet`**
- Add **VM1** and **VM2**
- Save

### ➤ Create Health Probe
- Name: `hp`
- Protocol: TCP
- Port: 80
- Save

### ➤ Add Load Balancing Rule
- Name: `LBrule`
- **Frontend IP:** `ip`
- **Backend Pool:** `bpl`
- **Protocol:** TCP
- **Port:** 80
- **Backend Port:** 80
- Select **Health Probe:** `hp`
- Save

### ➤ Test
- Go to **Load Balancer Overview**
- Copy the Public IP
- Paste in browser → Web App should load via load balancer

---