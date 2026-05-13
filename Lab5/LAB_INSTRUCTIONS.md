# Lab5: DNS and Web Server Lab 

##  Overview
This lab demonstrates how to configure a web server and DNS server. PCs will access a hosted website using a hostname instead of an IP address through DNS name resolution.

---

##  Topology

```text

             Server
               |
               |
             Switch
               |
    -----------|-----------
    |                      |
   PC1                    PC2
```

---

##  Objectives

- Configure a server with HTTP and DNS services
- Create a simple web page
- Configure DNS name resolution using an A-record
- Configure PCs to use the server as their DNS server
- Access a website using a hostname in a web browser

---

#  Network Addressing Plan

| Device | IP Address | Subnet Mask | DNS Server |
|--------|-------------|--------------|-------------|
| Server | 192.168.1.50 | 255.255.255.0 | N/A |
| PC1 | 192.168.1.10 | 255.255.255.0 | 192.168.1.100 |
| PC2 | 192.168.1.20 | 255.255.255.0 | 192.168.1.100 |

---

#  Step-by-Step Instructions

## 1️⃣ Add Devices

- 🖥️ 2 PCs
- 🖧 1 Cisco 2960 Switch
- 🌐 1 Server

---

## 2️⃣ Connect Devices

Use **Copper Straight-Through** cables to connect all devices to the switch.

| Device | Switch Connection | Port |
|---------|-------------------|------|
| PC1 | Switch |  Fe0/1 |
| PC2 | Switch |  Fe0/2 |
| Server | Switch | Fe0/24 |

---

## 3️⃣ Configure IP Addresses

### Server

```text
IP Address: 192.168.1.50
Subnet Mask: 255.255.255.0
```

### PC1

```text
IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
DNS Server: 192.168.1.50
```

### PC2

```text
IP Address: 192.168.1.20
Subnet Mask: 255.255.255.0
DNS Server: 192.168.1.50
```

---

# Configure HTTP Service

On **Server1**:

```text
Services → HTTP
```

- Enable HTTP service
- Edit the default `index.html` page

### Example Web Page

```html
<h1>Welcome to My Web Server</h1>
<p>DNS and HTTP services are working correctly!</p>
```

---

#  Configure DNS Service

On **Server**:

```text
Services → DNS
```

### Enable DNS Service

Add the following A-record:

| Name | Type/Record | Address |
|------|------|----------|
| www.mylab.com | A | 192.168.1.50 |

---

#  Configure DNS on PCs

On each PC:

```text
Desktop → IP Configuration
```

Set the DNS server field to:

```text
192.168.1.50
```

---

# Test Name Resolution

On a PC:

```text
Desktop → Web Browser
```

Navigate to:

```text
http://www.mylab.com
Also test the website with the IP instead of the name. (192.168.1.50)
```

---

## Expected Result

The browser should successfully load the custom webpage hosted on Server0.

Example:

```text
Welcome to My Web Server
DNS and HTTP services are working correctly!
```

---

# Verification Commands

## Test Connectivity

On a PC Command Prompt:

```bash
ping 192.168.1.50
```

## Test DNS Resolution

```bash
ping www.mylab.com
```

---

# Key Skills Learned

- DNS Configuration
- HTTP Server Configuration
- DNS A-Records
- Name Resolution
- Browser Testing
- Basic Network Services

---

# Troubleshooting Tips

If the webpage does not load:

- Verify the DNS server field on each PC
- Confirm HTTP service is enabled
- Ensure DNS service is enabled
- Double-check the A-record points to the correct IP
- Verify all devices are on the same subnet
- Test connectivity using `ping`
---

# Problems I had:

- The website was not reachable when using ping or entering the IP or the name of the website into the web browser URL bar. The problem i had was that i did not configured the server with an IP address, i only added the IP address and name to the DNS record but forgot to also add the IP to the actual server to be able to reach it. 

---
=
# Technologies Used

- DNS
- HTTP
- IPv4 Networking
- Cisco 2960 Switch

---

> [!TIP]
> DNS translates hostnames into IP addresses, allowing users to access websites without memorizing numerical IPs.

---