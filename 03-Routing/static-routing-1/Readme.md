# Static Routing Configuration Lab

## 🎯 Objective

To manually configure IP addresses on routers and PCs and establish communication between two different LAN networks using static routing.

---

## 🌐 Network Topology

Two LAN networks connected through two routers.

- LAN 1 → 192.168.1.0/24
- LAN 2 → 192.168.2.0/24
- Router-to-Router → 192.168.3.0/24




---

## 🖥 IP Addressing (Manually Assigned)

### 🔹 LAN 1

PC1 → 192.168.1.2 /24  
PC2 → 192.168.1.3 /24  
Default Gateway → 192.168.1.4  

Router2 LAN Interface → 192.168.1.4  

---

### 🔹 LAN 2

PC3 → 192.168.2.2 /24  
PC4 → 192.168.2.3 /24  
Default Gateway → 192.168.2.4  

Router3 LAN Interface → 192.168.2.4  

---

### 🔹 Router-to-Router Network

Router2 → 192.168.3.2  
Router3 → 192.168.3.3  

---

##
[Download Static IP Lab](static-routing-lab.pkt)


