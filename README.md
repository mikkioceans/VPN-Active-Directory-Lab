# 🛡️ VPN with Active Directory Authentication (Lab Project)

This project demonstrates how to configure a **Windows Server VPN (RRAS)** integrated with **Active Directory (AD)** for centralized authentication simulating how corporate organizations handle secure remote access for employees.

---

## 🚀 Project Overview
- **Domain Controller (Windows Server 2022)** → Active Directory & DNS
- **VPN Server (Windows Server 2022 with RRAS)** → VPN endpoint
- **Client Windows 10 Pro** → Test machine for remote connections
- **Domain** → `mikkioceans.local`


- VPN Clients authenticate using **Active Directory credentials**.
- RRAS assigns **internal IP addresses** to remote users.
- Remote users gain secure access to domain resources.

---

## 🔧 Implementation Steps

### 1️⃣ Active Directory Setup
- Installed AD DS and promoted server to Domain Controller.
- Created `VPN_Users` Organizational Unit.
- Added test users (`ppogba`, `bfernandes`) to `VPNUsers`.

### 2️⃣ Install RRAS (Remote Access)
- Installed the **Remote Access** role.
- Selected **DirectAccess and VPN (RAS)**.
- Chose **Custom configuration → VPN access**.

### 3️⃣ Configure RRAS
- Set IP address assignment:
  - Static pool: `192.168.0.105 – 192.168.0.110`
- Configured authentication:
  - **Windows Authentication** (Active Directory).
- Allowed users VPN access via ADUC (*Dial-in tab*).

### 4️⃣ Client Setup (Windows 10/11)
- *Settings → Network & Internet → VPN → Add VPN*  
  - VPN Provider: **Windows (built-in)**
  - Server: `vpn.mikkioceans.local` (or public IP)
  - Type: **PPTP**, **L2TP/IPsec**, or **SSTP**
  - Credentials: AD username + password

### 5️⃣ Testing
- Connected from client and verified:
  - VPN adapter received internal IP.
  - Successful ping to Domain Controller.
  - Access to internal shares (`\\dc1\share`).

---

## 🔒 Security Hardening
- Migrated from PPTP → L2TP/IPsec (pre-shared key).
- Configured SSTP with certificates for TLS security.
- Enforced access policies via **NPS (Network Policy Server)**.
- Recommended integration with **MFA** (e.g., Duo, Azure MFA).

---

## 📸 Screenshots
See `/screenshots` for detailed setup steps:
- AD setup
- RRAS installation
- RRAS configuration
- Client VPN connection
- Successful test results

---

## 🛠️ Skills Demonstrated
- Active Directory & Group Policy Management
- VPN configuration with RRAS
- Windows Server administration
- Security hardening & authentication policies

---

## 🔗 Future Enhancements
- Add **Always On VPN** for seamless corporate remote access
- Integrate **Azure MFA** for multi-factor authentication
- Experiment with firewall appliances (pfSense / FortiGate) instead of RRAS


