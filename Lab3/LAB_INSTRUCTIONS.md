# Lab3: DHCP Server Setup

## Overview
This lab demonstrates how to configure a Cisco router as a DHCP server so that PCs can automatically receive IP addressing information such as IP address, subnet mask, default gateway and DNS.
---

## Topology

```text 
         Router[DHCP pool]
               |
  Switch-------|--------Switch
    |                     |
   PC1                   PC2
```
## Objectives

- Configure a router as a DHCP server
- Exclude specific IP addresses from DHCP allocation
- Create DHCP pools for multiple subnets
- Configure DNS and default gateway settings
- Verify DHCP functionality
---

## Network Configuration

| Device | Interface  | IP Address     |
|--------|------------|----------------|
| R0     | G0/0       | 192.168.1.0/24 |
| R0     | G0/1       | 192.168.2./24  |
| PC1    | DHCP       | Automatic      |
| PC2    | DHCP       | Automatic      |

---

#  Step-by-Step Configuration

## 1️⃣ Configure Router Interfaces

```bash
enable
configure terminal

interface g0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface g0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
```

---

## 2️⃣ Exclude Addresses from DHCP Pools

Exclude the first 10 IP addresses in each subnet.

```bash
ip dhcp excluded-address 192.168.1.1 192.168.1.10
ip dhcp excluded-address 192.168.2.1 192.168.2.10
```

---

## 3️⃣ Create DHCP Pool for LAN1

```bash
ip dhcp pool LAN1
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 8.8.8.8
exit
```

---
## 4️⃣ Create DHCP Pool for LAN2

```bash
ip dhcp pool LAN2
network 192.168.2.0 255.255.255.0
default-router 192.168.2.1
dns-server 8.8.8.8
exit
```

---
## Configure PCs for DHCP

On both PCs:

```text
Desktop → IP Configuration → DHCP
```
The PCs should automatically receive:

- IP Address
- Subnet Mask
- Default Gateway
- DNS Server

---

##  Verification

Open Command Prompt on each PC and run:

```bash
ipconfig /all
```

### Expected Result

Each PC should display:

- A valid IP address from the correct subnet
- Default gateway configured
- DNS server set to `8.8.8.8`

Example:

```text
IP Address: 192.168.1.x
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
DNS Server: 8.8.8.8
```

---

##  Useful CLI Commands

### View DHCP Bindings

```bash
show ip dhcp binding
```

### View DHCP Pool Information

```bash
show ip dhcp pool
```

### View Running Configuration

```bash
show running-config
```

---

##  Key Skills Learned

- DHCP Configuration
- Dynamic IP Addressing
- Cisco Router Configuration
- DHCP Excluded Addresses
- Network Verification Commands

---

##  Troubleshooting Tips

If a PC shows `0.0.0.0` after enabling DHCP:

- Click **Fast Forward Time (>>|)** in Packet Tracer
- Ensure router interfaces are enabled with `no shutdown`
- Verify DHCP pools are configured correctly
- Check cable connections
- Confirm PCs are set to DHCP mode

---

##  Technologies Used
- CLI
- DHCP
- IPv4 Networking

---