#Lab 7: Router-on-a-Stick (Inter-VLAN Routing)

##  Overview
This lab demonstrates how to enable communication between multiple VLANs using a router-on-a-stick configuration. Inter-VLAN routing is achieved through router subinterfaces and 802.1Q trunking between the switch and router.

---

## 🌐 Topology

```text
                 ┌──────────────────────┐
                 │        Router0       │
                 │                      │
                 │ Gi0/0.10 → VLAN 10  │
                 │ 192.168.10.1        │
                 │                      │
                 │ Gi0/0.20 → VLAN 20  │
                 │ 192.168.20.1        |
                 |                     |
                 | Gi0/0.30 → VLAN 30  │
                 │ 192.168.30.1        |
                 |                     |        
                 | Gi0/0.40 → VLAN 40  │
                 │ 192.168.40.1        │
                 └──────────┬───────────┘
                            │
                      [802.1Q Trunk]
                            │
                        Switch
  ┌─────────────────┐────────────────┐────────────────┐  
  │                 │                |                |
VLAN 10           VLAN 20          VLAN 30          VLAN 40
```

---

## Objectives

- Configure a trunk port between the switch and router
- Create router subinterfaces for each VLAN
- Configure 802.1Q encapsulation
- Configure default gateways for VLANs
- Enable communication between VLANs
- Verify successful inter-VLAN routing

---

# Network Addressing Plan

| Device | VLAN | IP Address | Default Gateway |
|--------|------|-------------|------------------|
| Accounting PC1 | VLAN 10 | 192.168.10.10 | 192.168.10.1 |
| Accounting PC2 | VLAN 10 | 192.168.10.11 | 192.168.10.1 |
| IT PC1 | VLAN 20 | 192.168.20.10 | 192.168.20.1 |
| IT PC2 | VLAN 20 | 192.168.20.11 | 192.168.20.1 |
| HR PC1 | VLAN 30 | 192.168.30.10 | 192.168.30.1 |
| HR PC2 | VLAN 30 | 192.168.30.11 | 192.168.30.1 |
| Sales PC1 | VLAN 40 | 192.168.40.10 | 192.168.40.1 |
| Sales PC2 | VLAN 40 | 192.168.40.11 | 192.168.40.1 |

---

# Step-by-Step Instructions

## 1️⃣ Add Devices

Re-use the switch and PCs from Lab 6 and add:

- 1 Cisco Router

---

## 2️⃣ Configure VLANs on the Switch

```bash
enable
configure terminal

vlan 10
name Sales

vlan 20
name IT
```

---

## 3️⃣ Assign Access Ports

### VLAN 10 Ports

```bash
interface range fa0/1 - 5
switchport mode access
switchport access vlan 10
exit
```

### VLAN 20 Ports

```bash
interface range fa0/6 - 10
switchport mode access
switchport access vlan 20
exit
```

### VLAN 30 Ports

```bash
interface range fa0/11 - 15
switchport mode access
switchport access vlan 30
exit
```

### VLAN 40 Ports

```bash
interface range fa0/16 - 20
switchport mode access
switchport access vlan 40
exit
```

---

# Configure the Trunk Port

Assume the router connects to `Fa0/24`.

```bash
interface fa0/24
switchport mode trunk
exit
```

---

# Router Configuration

## 4️⃣ Enable Parent Interface

```bash
enable
configure terminal

interface gigabitEthernet0/0
no shutdown
exit
```

---

## 5️⃣ Configure Subinterface for VLAN 10

```bash
interface gigabitEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit
```

---

## 6️⃣ Configure Subinterface for VLAN 20

```bash
interface gigabitEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit
```

---

# Configure PC IP Addresses

## VLAN 10 PCs

### PC1

```text
IP Address: 192.168.10.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.10.1
```

### PC2

```text
IP Address: 192.168.10.11
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.10.1
```

---

## VLAN 20 PCs

### PC1

```text
IP Address: 192.168.20.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.20.1
```

### PC2

```text
IP Address: 192.168.20.11
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.20.1
```

---

# Connectivity Testing

## Test Cross-VLAN Communication

From Accounting PC1:

```bash
ping 192.168.20.10
```

From IT PC1:

```bash
ping 192.168.10.10
```

---

## Expected Result

```text
Reply from 192.168.20.10: bytes=32 time<1ms TTL=127

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

---

# Useful CLI Commands

## Verify VLANs

```bash
show vlan brief
```

## Verify Trunk Port

```bash
show interfaces trunk
```

## Verify Router Interfaces

```bash
show ip interface brief
```

## View Routing Table

```bash
show ip route
```

---

# Key Skills Learned

- VLAN Trunking
- Router Subinterfaces
- 802.1Q Encapsulation
- Inter-VLAN Routing
- Default Gateway Configuration

---

# Troubleshooting Tips

If inter-VLAN pings fail:

- Verify the switch port is configured as a trunk
- Ensure VLAN IDs match encapsulation numbers
- Confirm PCs have correct default gateways
- Make sure the parent router interface uses `no shutdown`
- Use `show interfaces trunk` to verify trunk status

---

# Technologies Used

- Cisco Router
- Cisco 2960 Switch
- VLANs
- 802.1Q Trunking
- IPv4 Networking

---

---

> [!TIP]
> Subinterfaces will not function unless the parent interface (`Gi0/0`) is enabled using `no shutdown`.

---