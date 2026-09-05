# DHCP Snooping 

## Overview
DHCP Snooping is a **Layer 2 security feature** on Cisco switches that protects the network from **Rogue DHCP Servers**. It identifies trusted and untrusted ports and allows DHCP server responses only through trusted interfaces.

It also creates a **DHCP Snooping Binding Table** containing:
- MAC Address
- IP Address
- VLAN
- Interface
- Lease Time

## 🎯 Objective
- Prevent Rogue/Fake DHCP Servers
- Protect clients from receiving malicious network configurations
- Learn trusted and untrusted switch ports
- Understand DHCP Snooping Binding Tables

## 🔑 Trusted vs Untrusted Ports

**Trusted Port:**  
The interface connected toward the legitimate DHCP Server or the network path leading to it.

**Untrusted Port:**  
Client/user-facing interfaces. They are **untrusted by default**.

Example:

    Legitimate DHCP Server
             |
             | TRUSTED
             ↓
           SWITCH
         /    |    \
        ↓     ↓     ↓
       PC1   PC2   PC3
      UNTRUSTED PORTS

## ⚙️ Configuration

### 1. Enable DHCP Snooping Globally

    Switch(config)# ip dhcp snooping

### 2. Enable DHCP Snooping for VLANs

    Switch(config)# ip dhcp snooping vlan 10,20,30

### 3. Configure the Legitimate DHCP Server/Uplink Port as Trusted

Example: Fa0/1 is connected toward the legitimate DHCP Server/router.

    Switch(config)# interface fa0/1
    Switch(config-if)# ip dhcp snooping trust

Client-facing ports remain **untrusted by default**.

## 🔍 Verification Commands

Check DHCP Snooping configuration:

    Switch# show ip dhcp snooping

Check learned DHCP bindings:

    Switch# show ip dhcp snooping binding

Example Binding Table:

    MacAddress        IpAddress        VLAN    Interface
    -----------------------------------------------------
    0011.2233.4455    192.168.10.10    10      Fa0/2
    0066.7788.9900    192.168.10.11    10      Fa0/3

## 🧠 How DHCP Snooping Works

1. Client sends a DHCP Discover.
2. Switch receives the DHCP request on an untrusted port.
3. Request is forwarded toward the trusted DHCP Server.
4. DHCP Server sends the response back.
5. Switch accepts DHCP server responses only from the trusted interface.
6. Switch records the client information in the DHCP Snooping Binding Table.
7. Rogue DHCP responses arriving from untrusted ports are dropped.

## 🚨 Security Problem Without DHCP Snooping

A Rogue DHCP Server can provide clients with:
- Fake IP addresses
- Malicious Default Gateway
- Malicious DNS Server
- Incorrect network configuration

This can potentially allow attackers to redirect or intercept network traffic.

## 🛡️ With DHCP Snooping

    Legitimate DHCP Server
             ↓
        TRUSTED PORT
             ↓
           SWITCH
          /  |  \
         ↓   ↓   ↓
       PC1  PC2  PC3
       ❌    ❌    ❌
     Rogue DHCP responses
       are blocked

## 📚 Important Commands

    ip dhcp snooping
    ip dhcp snooping vlan 10,20,30
    ip dhcp snooping trust
    show ip dhcp snooping
    show ip dhcp snooping binding

## 📝 Key Takeaways

- DHCP Snooping protects against **Rogue DHCP Servers**.
- DHCP Snooping is a **Layer 2 security feature**.
- Ports are **untrusted by default**.
- The port toward the legitimate DHCP Server should be **trusted**.
- DHCP responses from untrusted ports are blocked.
- DHCP Snooping creates a **binding table**.
- The binding table maps **MAC Address → IP Address → VLAN → Interface**.


## 💡 One-Line Revision

**DHCP Snooping = Trust the DHCP Server direction, block unauthorized DHCP responses, and build a binding table.**