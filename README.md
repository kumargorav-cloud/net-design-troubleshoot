# 🚀 Enterprise Multi-Site Network: Design, Security & Troubleshooting

## 📌 Overview

This project simulates a real-world enterprise network with a **Head Office (HQ)** and a **Branch Office**, focusing on network design, routing, security, and structured troubleshooting.

The network is implemented using **Cisco Packet Tracer** and includes VLAN segmentation, dynamic routing (OSPF), NAT for internet access, and ACL-based security.

---

## 🏗️ Network Architecture

* **HQ (Mumbai)**

  * VLAN-based segmentation (HR, IT, Guest)
  * Inter-VLAN routing (Router-on-a-Stick)
  * NAT (PAT) for internet access

* **Branch (Kolkata)**

  * Local LAN network
  * Connected to HQ via WAN link

* **WAN**

  * OSPF (Area 0) for dynamic routing between HQ and Branch

* **Internet (ISP)**

  * Simulated external network
  * Connected to HQ router (centralized internet breakout)

---

## 🌐 IP Addressing Scheme

### 🔹 VLAN Networks (HQ)

| VLAN | Department | Subnet          | Gateway      |
| ---- | ---------- | --------------- | ------------ |
| 10   | HR         | 192.168.10.0/24 | 192.168.10.1 |
| 20   | IT         | 192.168.20.0/24 | 192.168.20.1 |
| 30   | Guest      | 192.168.30.0/24 | 192.168.30.1 |

---

### 🔹 Branch Network

| Network    | Subnet          | Gateway      |
| ---------- | --------------- | ------------ |
| Branch LAN | 192.168.40.0/24 | 192.168.40.1 |

---

### 🔹 WAN Links

| Link          | Subnet       | Devices                      |
| ------------- | ------------ | ---------------------------- |
| R1 ↔ R2       | 10.0.12.0/30 | R1: 10.0.12.1, R2: 10.0.12.2 |
| R1 ↔ R3 (ISP) | 10.0.13.0/30 | R1: 10.0.13.1, R3: 10.0.13.2 |

---

### 🔹 Internet Network

| Network     | Subnet     |
| ----------- | ---------- |
| ISP Network | 8.8.8.0/24 |

---

## ⚙️ Technologies Used

* VLANs & Trunking
* Inter-VLAN Routing
* OSPF (Open Shortest Path First)
* NAT (PAT)
* Access Control Lists (ACL)
* DHCP
* ICMP (Ping, Traceroute)

---

## 🔐 Security Implementation

* Implemented **ACL on Guest VLAN**
* Restricted access:

  * Guest ❌ HR
  * Guest ❌ IT
  * Guest ❌ Branch
* Allowed:

  * Guest ✔ Internet access

---

## 🔁 Routing Design

* OSPF (Area 0) used between HQ and Branch
* Default route configured on HQ toward ISP
* Default route propagated to Branch using:

  * `default-information originate`

---

## 🌍 NAT Configuration

* NAT (PAT) configured on **HQ router**
* Inside interfaces:

  * VLAN subinterfaces
  * Branch-facing interface
* Outside interface:

  * ISP-facing interface

---

## 🧪 Problem Scenarios Simulated

### 🔴 1. OSPF Failure

* Missing network statement
* Result: No route to branch network

---

### 🔴 2. NAT Misconfiguration

* Incorrect inside/outside interface roles
* Result: Internet not reachable

---

### 🔴 3. Return Path Issue

* Missing route on ISP router
* Result: Ping fails despite correct forward routing

---

### 🔴 4. VLAN Misconfiguration

* Trunk misconfiguration
* Result: Hosts cannot reach gateway

---

### 🔴 5. ACL Misconfiguration

* Incorrect rule order or overly restrictive rules
* Result: Legitimate traffic blocked

---

## 🧠 Troubleshooting Methodology

A structured **OSI-layer approach** was used:

1. **Layer 1 (Physical)**

   * Interface status (`show ip interface brief`)

2. **Layer 2 (Switching)**

   * VLAN assignment (`show vlan brief`)
   * Trunk verification (`show interfaces trunk`)

3. **Layer 3 (Routing)**

   * Routing table (`show ip route`)
   * OSPF neighbors (`show ip ospf neighbor`)

4. **Services**

   * NAT (`show ip nat translations`)
   * DHCP (`ipconfig` on end devices)

5. **Security**

   * ACL verification (`show access-lists`)

---

## 🔍 Key Verification Commands

```
show ip route
show ip ospf neighbor
show ip nat translations
show vlan brief
show interfaces trunk
```

---

## 📈 Outcome

* Achieved secure VLAN-based segmentation
* Enabled dynamic routing between HQ and Branch
* Provided internet access via NAT
* Implemented guest network isolation
* Developed strong troubleshooting skills using structured methodology

---

## 🎯 Key Learning

This project demonstrates the ability to:

* Design scalable enterprise networks
* Implement routing and security policies
* Troubleshoot real-world network failures effectively

---
