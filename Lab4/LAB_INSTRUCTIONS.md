#  Lab 4: Small Office LAN Design

## Overview
This lab demonstrates how to design and configure a small office Local Area Network (LAN). The network consists of four PCs and one network printer connected through a single switch in a flat network topology.

---

##  Topology

```
            Printer
               |
               |
            Switch
               |
    -----------|-----------
    |      |       |      |
   PC1    PC2     PC3    PC4
```

---

## Objectives

- Build a small office LAN
- Connect multiple devices using a switch
- Configure static IPv4 addressing
- Test end-to-end connectivity between all devices
- Verify successful communication using `ping`

---

# Network Addressing Plan

| Device  | IP Address | Subnet Mask   | 
|---------|------------|---------------|
| PC1     | 10.0.0.11  | 255.255.255.0 |
| PC2     | 10.0.0.12  | 255.255.255.0 |
| PC3     | 10.0.0.13  | 255.255.255.0 |
| PC4     | 10.0.0.14  | 255.255.255.0 |
| Printer | 10.0.0.50  | 255.255.255.0 |

---

# Step-by-Step Instructions

## 1️⃣ Add Devices

- 🖥️ 4 PCs
- 🖨️ 1 Printer
- 🔀 1 Cisco 2960 Switch

---

## 2️⃣ Connect Devices

Use **Copper Straight-Through** cables to connect all devices to the switch.

| Device  | Switch Port |
|---------|-------------|
| PC1     | Fa0/1       |
| PC2     | Fa0/2       |
| PC3     | Fa0/3       |
| PC4     | Fa0/4       |
| Printer | Fa0/24       |

---

## 3️⃣ Configure IP Addresses

### On Each PC

```text
Desktop → IP Configuration
```
Assign the corresponding IP address and subnet mask.

### Example Configuration for PC1

```text
IP Address: 10.0.0.11
Subnet Mask: 255.255.255.0
```

Repeat the process for all devices using the addressing table above.

---

## Configure Printer

On the printer:

```text
Config → FastEthernet0
```

Assign:

```text
IP Address: 10.0.0.50
Subnet Mask: 255.255.255.0
```

---

# Connectivity Testing

On each PC:

```text
Desktop → Command Prompt
```

Use the `ping` command to test connectivity with:

- Other PCs
- Printer

### Example

```bash
ping 10.0.0.50
```

---

## Expected Results

Successful communication should display:

```text
Reply from 10.0.0.50: bytes=32 time<1ms TTL=128
Reply from 10.0.0.50: bytes=32 time<1ms TTL=128
Reply from 10.0.0.50: bytes=32 time<1ms TTL=128
Reply from 10.0.0.50: bytes=32 time<1ms TTL=128

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

---

# Useful CLI Commands

## View Learned MAC Addresses on the Switch

```bash
show mac address-table
```

---

# Key Skills Learned

- LAN Design
- IPv4 Addressing
- Flat Network Configuration
- Switch Connectivity
- End-to-End Connectivity Testing
- Basic Network Troubleshooting

---

# Troubleshooting Tips

If connectivity fails:

- Verify all cables are connected correctly
- Ensure all devices are in the same subnet
- Double-check IP addresses for typing errors
- Confirm the switch ports are active
- Wait a few seconds for MAC address learning

---

# Technologies Used

- Cisco 2960 Switch
- IPv4 Networking
- Ethernet LAN

---

> [!TIP]
> Documenting your IP addressing plan in a notepad or spreadsheet is a great networking habit and helps simplify troubleshooting.
---