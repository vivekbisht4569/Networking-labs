# 🏦 SecureTrust Banking Infrastructure Network

##  Project Overview

This project demonstrates the implementation of an enterprise-style banking network infrastructure using Cisco Packet Tracer.  
The network was designed to simulate real-world enterprise networking concepts including VLAN segmentation, Inter-VLAN Routing, DHCP, STP security, and centralized network management.

The project focuses on building a scalable, secure, and organized network environment for different banking departments.

---

#  Technologies Used

- Cisco Packet Tracer
- VLANs
- VLAN Trunking
- Router-On-A-Stick (ROAS)
- DHCP Server
- DHCP Relay (IP Helper Address)
- Spanning Tree Protocol (STP)
- Root Bridge Election
- Root Guard
- Inter-VLAN Routing
- Enterprise Switching

---

#  Network Topology

## Devices Used

| Device | Model |
|---|---|
| Router | Cisco 2811 |
| Core Switch | Cisco 3560 |
| Access Switches | Cisco 2960 |
| DHCP Server | Server-PT |
| End Devices | PCs & Laptops |

---

#  VLAN Design

| VLAN | Department | Network |
|---|---|---|
| VLAN 10 | Customer Support | 192.168.10.0/24 |
| VLAN 20 | Accounts | 192.168.20.0/24 |
| VLAN 30 | Loans | 192.168.30.0/24 |
| VLAN 40 | IT Department | 192.168.40.0/24 |

---

#  VLAN Trunking

Trunk links were configured between switches and router interfaces to allow multiple VLANs to pass through a single physical connection using IEEE 802.1Q encapsulation.

### Example Configuration

```bash
interface fa0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40
```

---

#  Router-On-A-Stick (ROAS)

Inter-VLAN communication was achieved using Router-On-A-Stick (ROAS).

A single router interface was divided into multiple subinterfaces, each configured for a different VLAN.

## Router Configuration

```bash
conf t

interface g0/0
no shutdown

interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
ip helper-address 192.168.40.10

interface g0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
ip helper-address 192.168.40.10

interface g0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
ip helper-address 192.168.40.10

interface g0/0.40
encapsulation dot1Q 40
ip address 192.168.40.1 255.255.255.0
```

---

#  DHCP Server Configuration

A centralized DHCP server was implemented to automatically assign IP addresses across all VLANs.

Multiple DHCP pools were created for different VLANs.

## DHCP Features

- Automatic IP Assignment
- Centralized IP Management
- DHCP Relay using IP Helper Address
- Dynamic Network Configuration

---

#  Spanning Tree Protocol (STP)

STP was implemented to prevent Layer 2 switching loops and maintain network stability.

## STP Design

| Switch | Role |
|---|---|
| Core Switch (3560) | Root Bridge |
| Access Switch (2960) | Secondary Root |

### Root Bridge Configuration

```bash
spanning-tree vlan 1 priority 4096
```

### Secondary Root Configuration

```bash
spanning-tree vlan 1 priority 8192
```

---

#  Root Guard Security

Root Guard was configured to prevent rogue switches from becoming the Root Bridge of the network.

When a superior BPDU was received on protected ports, the interface entered:

```text
root-inconsistent state
```

This protected the STP topology from unauthorized manipulation.

### Root Guard Configuration

```bash
interface fa0/10
spanning-tree guard root
```

---

#  Features Implemented

- VLAN Segmentation
- VLAN Trunking
- Inter-VLAN Routing
- DHCP Server Configuration
- DHCP Relay Agent
- STP Root Bridge Election
- Root Guard Security
- Enterprise Network Topology
- Centralized IP Management
- Network Scalability

---

#  Verification Performed

## VLAN Verification

```bash
show vlan brief
```

## Trunk Verification

```bash
show interfaces trunk
```

## STP Verification

```bash
show spanning-tree
```

## Router Interface Verification

```bash
show ip interface brief
```

## DHCP Verification

PCs successfully received IP addresses dynamically from the DHCP server.

## Connectivity Testing

Successful ping tests were performed between devices in different VLANs.

---

#  Screenshots Included

- Full Network Topology
- VLAN Configuration
- Trunk Configuration
- ROAS Configuration
- DHCP Pools
- DHCP Success Verification
- STP Root Bridge Verification
- Root Guard Verification
- Successful Inter-VLAN Ping Tests

---

#  Key Learnings

- Enterprise VLAN Design
- VLAN Segmentation
- Router-On-A-Stick Implementation
- DHCP Relay using IP Helper Address
- STP Root Bridge Election
- Root Guard Security
- Inter-VLAN Communication
- Layer 2 Security Concepts
- Enterprise Switching Architecture
- Network Troubleshooting

---

#  Skills Practiced

- Cisco CLI Configuration
- Network Troubleshooting
- Enterprise Switching
- Routing Concepts
- DHCP Configuration
- STP Security
- VLAN Management
- Inter-VLAN Routing

---

# Conclusion

This project provided practical hands-on experience in designing and implementing a secure enterprise banking infrastructure using Cisco technologies.

The lab improved understanding of:

1 VLAN segmentation  
2 Enterprise switching  
3 Inter-VLAN routing  
4 DHCP deployment  
5 STP security  
6 Root Guard implementation  
7 Enterprise network troubleshooting  

This project represents a strong foundation in networking and cybersecurity infrastructure concepts.

---