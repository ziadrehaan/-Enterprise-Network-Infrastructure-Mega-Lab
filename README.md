# 🏢 Enterprise Network Infrastructure – Mega Lab 

---
## 📌 Overview

This project simulates a full enterprise network design implemented in Cisco Packet Tracer. It focuses on segmenting departments using **VLANs**, implementing **inter-VLAN routing** with **Router-on-a-Stick**, **DHCP server configuration**, subnetting via **VLSM**, and adding **Layer 2 security features**.  
The network is scalable, secure, and reflects real-world enterprise setups.

---

## 🧱 Network Topology

The network consists of:

- 🛠️ 1 Router (Gateway + DHCP Server)  
- 🔌 1 Core Switch  
- 🧷 Multiple Access Switches  
- 💻 End Devices (PCs, printers, and servers)  
- 🧑‍💼 Four logical departments

> _📷 Insert diagram here: `topology.png`_

---

## 🧠 Subnetting Design

Main network used: `192.168.1.0/24`  
Applied **Variable Length Subnet Masking (VLSM)** to split into four subnets based on department size.

| Department  | Subnet ID       | Range (Usable IPs)             | Subnet Mask         | Hosts |
|-------------|------------------|---------------------------------|----------------------|--------|
| IT          | 192.168.1.0      | 192.168.1.1 – 192.168.1.62     | 255.255.255.192 (/26) | 62     |
| HR          | 192.168.1.64     | 192.168.1.65 – 192.168.1.126   | 255.255.255.192 (/26) | 62     |
| Sales       | 192.168.1.128    | 192.168.1.129 – 192.168.1.158  | 255.255.255.224 (/27) | 30     |
| Accounting  | 192.168.1.160    | 192.168.1.161 – 192.168.1.174  | 255.255.255.240 (/28) | 14     |

> _📷 Insert image here: `subnet-plan.png`_

---

## 🧮 IP Addressing Table

| Department  | Gateway           | Subnet Mask         | CIDR |
|-------------|-------------------|----------------------|------|
| IT          | 192.168.1.1       | 255.255.255.192      | /26  |
| HR          | 192.168.1.65      | 255.255.255.192      | /26  |
| Sales       | 192.168.1.129     | 255.255.255.224      | /27  |
| Accounting  | 192.168.1.161     | 255.255.255.240      | /28  |

---

## 🔐 VLAN Configuration

Each department is assigned to its own VLAN:

| VLAN ID | Department  |
|---------|-------------|
| 10      | IT          |
| 20      | HR          |
| 30      | Sales       |
| 40      | Accounting  |

- Access ports assigned to appropriate VLANs  
- Trunk port configured between router and switch for **Router-on-a-Stick**

---

## 🌐 Inter-VLAN Routing (Router-on-a-Stick)

Router configuration includes sub-interfaces for each VLAN:


interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.192

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.1.65 255.255.255.192

interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address 192.168.1.129 255.255.255.224

interface GigabitEthernet0/0.40
 encapsulation dot1Q 40
 ip address 192.168.1.161 255.255.255.240

✅ Each VLAN uses its sub-interface as a default gateway
✅ Devices can now communicate across VLANs

## 📡 DHCP Configuration

Dynamic IP addresses are assigned using the router's DHCP service:

ip dhcp excluded-address 192.168.1.1 192.168.1.10
ip dhcp excluded-address 192.168.1.65 192.168.1.70
ip dhcp excluded-address 192.168.1.129 192.168.1.130
ip dhcp excluded-address 192.168.1.161 192.168.1.162

ip dhcp pool IT
network 192.168.1.0 255.255.255.192
default-router 192.168.1.1
dns-server 192.168.1.200

ip dhcp pool HR
network 192.168.1.64 255.255.255.192
default-router 192.168.1.65
dns-server 192.168.1.200

ip dhcp pool Sales
network 192.168.1.128 255.255.255.224
default-router 192.168.1.129
dns-server 192.168.1.200

ip dhcp pool Accounting
network 192.168.1.160 255.255.255.240
default-router 192.168.1.161
dns-server 192.168.1.200


🔧 Reserved ranges for gateways and servers  
🔧 Local DNS Server IP: 192.168.1.200

---

## 🛡️ Security Measures

### ✅ Port Security
- Limits max devices per port to **2**
- Enables **sticky MAC**
- Prevents **unauthorized connections**

### ✅ DHCP Snooping
- Blocks **rogue DHCP servers**
- Only **uplink ports** are trusted

### ✅ Dynamic ARP Inspection (DAI)
- Prevents **ARP spoofing**
- Relies on **DHCP snooping binding table**

### ✅ BPDU Guard & PortFast
- Prevents **Spanning Tree Protocol attacks**
- Enables **fast startup** for access ports

---

## 🗂️ Project Files

| File                  | Description                       |
|-----------------------|-----------------------------------|
| `EnterpriseNetwork.pkt` | Main Cisco Packet Tracer project |
| `topology.png`         | Network topology diagram         |
| `subnet-plan.png`      | Subnetting and IP planning chart |
| `Documentation.pdf`    | Full technical documentation     |
| `README.md`            | Project documentation (this file)|

---

## ✅ Conclusion

The enterprise network simulation was successfully built with:

- ✅ **Subnetting** for efficient address management  
- ✅ **VLANs and Router-on-a-Stick** for inter-department communication  
- ✅ **DHCP** for automated IP assignment  
- ✅ **Security mechanisms** to protect the internal infrastructure  

This setup demonstrates best practices for scalable, secure, and manageable enterprise networks and


[![image.png](https://i.postimg.cc/6Qbv6fBh/image.png)](https://postimg.cc/R3fFXf63)
<div align="right" [![image.png](https://i.postimg.cc/6Qbv6fBh/image.png)](https://postimg.cc/R3fFXf63)>
 
 <a href="mailto:zezorehan938@gmail.com">𝓩𝓲𝓪𝓭𝓻𝓮𝓱𝓪𝓪𝓷</a>  
</div>
