# Lab4: Small Office LAN Design

## OVERVIEW
Connect two separate subnets through a router and achieve inter-subnet routing.
## TOPOLOGY
```
         [Router]
          /    \
    Gi0/0        Gi0/1
      |            |
    [SW1]        [SW2]
      |            |
    [PC1]        [PC2]
```



## OBJECTIVES
1. **Initialize Workspace:** Add 1 router (1941), 2 switches, and 2 PCs.
2. **Cabling:** Connect PC1 to the Switch, then the Switch to the Router Gi0/0 interface.
3. **Addressing:** Connect PC2 to the Switch, then the Switch to the Router Gi0/1.
    * **PC1** → `192.168.1.10/24`
    * **PC2** → `192.168.2.10/24`
    * **Router Gi0/0** → 192.168.1.1/24
    * **Router Gi0/1** → 192.168.2.1/24
    **Bring both interfaces up with no shutdown**
4. **Testing:** Ping both PCs to each other and also ping the default gateways.
5. **Verification:** Confirm 4 successful replies with 0% packet loss when pinging each divice.
---

## CLI HINTS
```
R0# configure terminal
R0(config)# interface gi0/0
R0(config-if)# ip address 192.168.1.1 255.255.255.0
R0(config-if)# no shutdown
Repeat for Gi0/1. Set default gateways on PCs to router IPs.
```

## KEY SKILLS
* Router CLI
* Interface config
* Default gateway

> [!TIP]
> **PRO TIP:** Set each PC's default gateway to the router IP on its subnet or pings won't return.