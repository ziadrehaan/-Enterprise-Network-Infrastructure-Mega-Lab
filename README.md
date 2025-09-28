# 🏢 Enterprise Network Infrastructure – Mega Lab

**Author:** Ziad Rehan  
**Project Type:** CCNA Enterprise Network Simulation  
**Tool Used:** Cisco Packet Tracer

---

## 📚 Table of Contents

1. [Introduction](#1-introduction)  
2. [Network Topology](#2-network-topology)  
3. [Subnetting Design Explanation](#3-subnetting-design-explanation)  
4. [IP Addressing Scheme](#4-ip-addressing-scheme)  
5. [Inter-VLAN Routing (Router-on-a-Stick)](#5-inter-vlan-routing-router-on-a-stick)  
6. [DHCP Configuration](#6-dhcp-configuration)  
7. [Security Measures Implemented](#7-security-measures-implemented)  
8. [Conclusion](#8-conclusion)

---

## 1. Introduction

This project represents the design and implementation of a company's internal network infrastructure.

**Main Objectives:**
- Divide the network into departments using VLANs and subnetting.
- Provide dynamic IP addressing using DHCP.
- Enable inter-VLAN communication via Router-on-a-Stick.
- Apply Layer 2 security features to protect the network.

---

## 2. Network Topology

The network includes:
- One Router (acting as the default gateway and DHCP server)
- One Main Switch connected to the router
- Multiple Access Switches connected to the main switch
- End devices (PCs, printers, servers) distributed across departments

> _Network Diagram Placeholder_  
> *(Insert or link to topology.png)*

---

## 3. Subnetting Design Explanation

The main network `192.168.1.0/24` was divided into multiple subnets using VLSM:

### 🔹 IT Department
- Subnet ID: `192.168.1.0/26`
- Usable IPs: `192.168.1.1 – 192.168.1.62`
- Broadcast: `192.168.1.63`

### 🔹 HR Department
- Subnet ID: `192.168.1.64/26`
- Usable IPs: `192.168.1.65 – 192.168.1.126`
- Broadcast: `192.168.1.127`

### 🔹 Sales Department
- Subnet ID: `192.168.1.128/27`
- Usable IPs: `192.168.1.129 – 192.168.1.158`
- Broadcast: `192.168.1.159`

### 🔹 Accounting Department
- Subnet ID: `192.168.1.160/28`
- Usable IPs: `192.168.1.161 – 192.168.1.174`
- Broadcast: `192.168.1.175`

---

## 4. IP Addressing Scheme

| Department | Network Address | Subnet Mask (CIDR) | Usable IP Range               | Default Gateway   |
|------------|------------------|--------------------|-------------------------------|-------------------|
| IT         | 192.168.1.0      | /26                | 192.168.1.1 – 192.168.1.62     | 192.168.1.1       |
| HR         | 192.168.1.64     | /26                | 192.168.1.65 – 192.168.1.126   | 192.168.1.65      |
| Sales      | 192.168.1.128    | /27                | 192.168.1.129 – 192.168.1.158  | 192.168.1.129     |
| Accounting | 192.168.1.160    | /28                | 192.168.1.161 – 192.168.1.174  | 192.168.1.161     |

---

## VLANs Configuration

- **VLAN 10** – IT Department  
- **VLAN 20** – HR Department  
- **VLAN 30** – Sales Department  
- **VLAN 40** – Accounting Department

> Trunk ports are configured between the switches and the router for Router-on-a-Stick routing.  
> _VLAN diagram placeholder_  
> *(Insert or link to vlan-config.png)*

---

## 5. Inter-VLAN Routing (Router-on-a-Stick)

Router configuration sample:

```bash
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
