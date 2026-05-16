# Lab-6: VLAN Segmentation 

##  Overview
This lab demonstrates how to segment a switch into multiple VLANs to isolate network traffic. Devices within the same VLAN can communicate, while communication between different VLANs is blocked without a router or Layer 3 device.

---

## Topology

```text

  [PC-1] [PC-2] [PC-1] [PC-2]
        |             |
        |             |
        |             |
     [VLAN 10]     [VLAN 40]
          \           /
           \         /
            \       /
             Switch
            /       \ 
           /         \
          /           \
    [VLAN 20]      [VLAN 30]   
       |              |
       |              |
       |              |
  [PC-1] [PC-2] [PC-1] [PC-2]

---

## Objectives

- Create VLANs on a Cisco switch
- Assign switch ports to VLANs
- Configure PCs with static IP addresses
- Verify communication within VLANs
- Confirm isolation between VLANs

---

# Network Addressing Plan

| Device | VLAN | IP Address | Subnet Mask |
|--------|------|-------------|--------------|
| PC1 | VLAN 10 (Accounting) | 192.168.10.1 | 255.255.255.0 |
| PC2 | VLAN 10 (Accounting) | 192.168.10.2 | 255.255.255.0 |
| PC1 | VLAN 20 (IT) | 192.168.20.1 | 255.255.255.0 |
| PC2 | VLAN 20 (IT) | 192.168.20.2 | 255.255.255.0 |
| PC1 | VLAN 30 (HR) | 192.168.30.1 | 255.255.255.0 |
| PC2 | VLAN 30 (HR) | 192.168.30.2 | 255.255.255.0 |
| PC1 | VLAN 40 (Sales) | 192.168.40.1 | 255.255.255.0 |
| PC2 | VLAN 40 (Sales) | 192.168.40.2 | 255.255.255.0 |

---

# Step-by-Step Instructions

## 1️⃣ Add Devices

- 🖥️ 8 PCs - [2 Per VLAN]
- 🔀 1 Cisco Switch

---

## 2️⃣ Connect Devices

Use **Copper Straight-Through** cables.

| Device | Switch Port | VLAN |
|---------|-------------|------|
| PC1 | Fa0/1 | VLAN 10 |
| PC2 | Fa0/2 | VLAN 10 |
| PC1 | Fa0/6 | VLAN 20 |
| PC2 | Fa0/7 | VLAN 20 |
| PC1 | Fa0/11 | VLAN 30 |
| PC2 | Fa0/12 | VLAN 30 |
| PC1 | Fa0/16 | VLAN 40 |
| PC2 | Fa0/17 | VLAN 40 |

---

# Switch Configuration

Enter the following commands on the switch CLI.

---

## 3️⃣ Create VLAN 10 (Accounting)

```bash
enable
configure terminal

vlan 10
name Accounting
exit
```

---

## 4️⃣ Create VLAN 20 (IT)

```bash
vlan 20
name IT
exit
```

---

## 5️⃣ Assign Ports to VLAN 10

```bash
interface range fa0/1 - 5
switchport mode access
switchport access vlan 10
exit
```

---

## 6️⃣ Assign Ports to VLAN 20

```bash
interface range fa0/6 - 10
switchport mode access
switchport access vlan 20
exit
```

---

# Configure PC IP Addresses

On each PC:

```text
Desktop → IP Configuration
```

Assign IP addresses according to the addressing table.

---

# Connectivity Testing

## Same VLAN Communication

### From PC1 [Accounting]

```bash
ping 192.168.10.2
```

### From PC1 [IT]

```bash
ping 192.168.20.2
```

Expected Result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
NOTE: You are pinging the second PC in the same VLAN or department if there is an error when pinging check the VLAN access ports 
```

---

## Cross-VLAN Communication

### From PC1 [Accounting]

```bash
ping 192.168.20.1
```

Expected Result:

```text
Request timed out.
Since You are pinging a computer on VLAN 20 [IT] from the VLAN 10 [Accounting], you are gonna get a timed out result 
```

or

```text
Packets: Sent = 4, Received = 0, Lost = 4 (100% loss)
```

---

#  Useful CLI Commands

## Verify VLAN Assignments

```bash
show vlan brief
```

## View Running Configuration

```bash
show running-config
```

---

#  Key Skills Learned

- VLAN Creation
- VLAN Port Assignment
- Switchport Configuration
- Network Segmentation
- Traffic Isolation

---

#  Troubleshooting Tips

If devices cannot communicate:

- Verify ports are assigned to the correct VLAN
- Confirm IP addresses are in the correct subnet
- Use `show vlan brief` to verify VLAN membership
- Ensure cables are connected correctly
- Confirm interfaces are active

---

#  Technologies Used

- Cisco Switch
- VLANs
- IPv4 Networking
- Ethernet Switching 

---

---

> [!TIP]
> VLANs isolate broadcast domains on a switch. Without a router or Layer 3 switch, devices in different VLANs cannot communicate.
> Use this command to assign 
> SW(config)# vlan 10
> SW(config-vlan)# name Accounting
> SW(config)# interface fa0/1
> SW(config-if)# switchport mode access
> SW(config-if)# switchport access vlan 10
> Use show vlan brief to confirm assignments.
---