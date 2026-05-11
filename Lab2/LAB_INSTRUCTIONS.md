# Lab2:  Router Interface Configuration

## 📌 Overview
This lab demonstrates how to connect two separate networks using a Cisco router and configure inter-subnet routing. Devices on different subnets will communicate through the router interfaces acting as default gateways.

---

## Topology
``text
PC1 ── SW ── Router Gi0/0
                     |
                     |
                  Router Gi0/1 ── SW1 ── PC2
```

---

## Objectives

- Add 1 router, 2 switches, and 2 PCs
- Configure separate IPv4 subnets
- Connect networks through a router
- Configure router interfaces using Cisco IOS CLI
- Enable routing between subnets
- Verify connectivity using `ping`

---

# Network Addressing Plan

| Device | Interface          | IP Address   | Subnet Mask   | Default Gateway  |
|--------|--------------------|------------- |---------------|------------------|
| PC1    | FastEthernet0      | 192.168.1.10 | 255.255.255.0 | 192.168.1.1      |
| Router | GigabitEthernet0/0 | 192.168.1.1  | 255.255.255.0 | N/A              |
| Router | GigabitEthernet0/1 | 192.168.2.1  | 255.255.255.0 | N/A              |
| PC2    | FastEthernet0      | 192.168.2.10 | 255.255.255.0 | 192.168.2.1      |

---

# Step-by-Step Instructions

## 1️⃣ Add Devices

- 🖥️ 2 PCs
- 🔀 2 Cisco 2960 Switches
- 📡 1 Cisco 1941 Router

---

## 2️⃣ Connect Devices

Use **Copper Straight-Through** cables.

| From    | To                    |
|---------|-----------------------|
| PC0     | Switch0               |
| Switch0 | R0 GigabitEthernet0/0 |
| PC1     | Switch1               |
| Switch1 | R0 GigabitEthernet0/1 |

---

## 3️⃣ Configure PC IP Addresses

### PC0

```text
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
```

### PC1

```text
IP Address: 192.168.2.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.2.1
```
---

#  Router Configuration

Enter the following commands on the router CLI:

```bash
enable
configure terminal

interface gigabitEthernet0/0
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

interface gigabitEthernet0/1
ip address 192.168.2.1 255.255.255.0
no shutdown
exit
```

---

# Connectivity Test

On PC0:

```text
Desktop → Command Prompt
```

Run:

```bash
ping 192.168.2.10
```

---

## Expected Result

```text
Reply from 192.168.2.10: bytes=32 time<1ms TTL=127
Reply from 192.168.2.10: bytes=32 time<1ms TTL=127
Reply from 192.168.2.10: bytes=32 time<1ms TTL=127
Reply from 192.168.2.10: bytes=32 time<1ms TTL=127

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

---

# Useful CLI Commands

## View Interface Status

```bash
show ip interface brief
```

## View Running Configuration

```bash
show running-config
```

## Verify Routing Table

```bash
show ip route
```

---

#  Key Skills Learned

- Router CLI Configuration
- Interface Configuration
- IPv4 Addressing
- Default Gateway Configuration
- Inter-Subnet Routing

---

# Troubleshooting Tips

If the ping fails:

- Verify router interfaces are enabled using `no shutdown`
- Check PC default gateways
- Ensure IP addresses are configured correctly
- Confirm cables are connected properly
- Verify both PCs are in different subnets

---

# Technologies Used

- Cisco 1941 Router
- Cisco 2960 Switch
- IPv4 Networking
- Inter-Subnet Routing

---

# Suggested Screenshots

Include screenshots of:

- Completed topology
- Router CLI configuration
- Successful ping results
- `show ip interface brief` output

---

> [!TIP]
> Each PC must use the router interface on its subnet as the default gateway or return traffic will fail.

---