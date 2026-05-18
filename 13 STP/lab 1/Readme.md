# 🌐 Spanning Tree Protocol (STP) Root Guard Security Lab

##  Overview

This lab demonstrates how a rogue/attacker switch can manipulate the **Spanning Tree Protocol (STP)** election process by advertising a lower bridge priority and becoming the **Root Bridge** of the network.

The lab also demonstrates how to secure the network using **Root Guard**, preventing unauthorized switches from taking control of the STP topology.

---

#  Concepts Covered

- Spanning Tree Protocol (STP)
- Root Bridge Election
- Bridge Priority
- Rogue / Attacker Switch
- Root Guard
- Root-Inconsistent State
- STP Security
- Layer 2 Attack Prevention

---

#  Network Topology

##  Initial Network

- **S2** configured as Root Bridge
- **S1** configured as Backup Root Bridge
- **S3** connected in redundant topology
- PCs connected for traffic testing

---

##  Attack Scenario

An attacker switch was connected to the network with the following configuration:

```bash
spanning-tree vlan 1 priority 0
```

This forced the attacker switch to advertise the **lowest bridge priority**, allowing it to become the new Root Bridge.

---

#  Initial STP Configuration

##  Configure Root Bridge on S2

```bash
conf t
spanning-tree vlan 1 priority 4096
```

---

##  Configure Backup Root on S1

```bash
conf t
spanning-tree vlan 1 priority 8192
```

---

#  Verification

##  Verify Root Bridge

```bash
show spanning-tree
```

###  Expected Output

```text
This bridge is the root
```

---

#  Task 1 — Simulating STP Attack

##  Objective

Simulate a rogue switch attempting to take control of the STP topology by advertising the lowest bridge priority.

---

##  Configure Attacker Switch

```bash
conf t
spanning-tree vlan 1 priority 0
```

---

##  Verify Attack Success

```bash
show spanning-tree
```

---

#  Observations

After the attacker switch became Root Bridge:

- STP recalculated topology
- Traffic paths changed
- Some ports entered blocking state
- Network traffic started flowing through attacker switch

This demonstrates how a rogue switch can manipulate Layer 2 topology and potentially intercept traffic.

---

#  Task 2 — Securing the Network with Root Guard

##  Objective

Prevent unauthorized switches from becoming Root Bridge.

---

##  Remove Attacker Links

Disconnect the attacker switch from:

- S2
- S3

---

##  Configure Root Guard on Trusted Ports

###  On S2

```bash
conf t
interface range g1/0/1 - 24
spanning-tree guard root
```

---

###  On S3

```bash
conf t
interface range g1/0/1 - 24
spanning-tree guard root
```

---

##  Reconnect Attacker Switch

Reconnect the attacker switch back into the network.

---

#  Verification

```bash
show spanning-tree
```

---

##  Expected Result

Ports connected to the attacker switch move into:

```text
root-inconsistent state
```

This prevents the attacker switch from becoming Root Bridge.

---

#  Final Outcome

-  Attacker switch failed to become Root Bridge
-  Original Root Bridge remained active
-  Root Guard protected STP topology
-  Unauthorized STP manipulation was prevented

---

#  Key Learning

##  Root Bridge Election

The switch with the **lowest Bridge ID** becomes Root Bridge.

---

##  Rogue Switch Attack

An attacker can manipulate STP by setting an extremely low bridge priority.

---

##  Root Guard

Root Guard prevents ports from accepting superior BPDUs from unauthorized switches.

---

##  Root-Inconsistent State

Ports receiving superior BPDUs are placed into **root-inconsistent state** instead of allowing topology changes.

---

##  Enterprise Security Importance

Layer 2 security is critical in enterprise environments to prevent:

- Traffic manipulation
- Rogue switches
- Topology hijacking
- Broadcast instability

---

# Verification Commands Used

##  Show STP Status

```bash
show spanning-tree
```

---

##  Show Running Configuration

```bash
show running-config | include spanning-tree
```

---

#  Lab Screenshots

##  Network Topology



---

##  Attacker Switch Becoming Root Bridge

_Add screenshot here_

---

##  Root Guard Blocking Rogue Switch

_Add screenshot here_

---

##  Root-Inconsistent State Verification

_Add screenshot here_

---

#  Technologies Used

- Cisco Packet Tracer
- Cisco 3650 Switches
- STP (Spanning Tree Protocol)
- PVST
- Root Guard

---

#  Skills Practiced

- STP Configuration
- Root Bridge Election
- Layer 2 Security
- Root Guard Deployment
- STP Troubleshooting
- Enterprise Switching Concepts

---

#  Conclusion

This lab provided practical understanding of:

✅ How STP works internally  
✅ How attackers can manipulate Layer 2 topology  
✅ How Root Guard protects enterprise networks  
✅ Real-world switch security implementation  

This was a valuable hands-on exercise for improving networking and cybersecurity fundamentals.

---

