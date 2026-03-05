# Router-on-a-Stick (ROAS) Lab

## Objective
The objective of this lab is to configure **inter-VLAN communication** using the **Router-on-a-Stick (ROAS)** method. A single router interface will be used to route traffic between multiple VLANs using subinterfaces.

---

## Topology

Devices used:

- 1 Router (Cisco ISR4321)
- 1 Switch (Cisco 2960)
- 3 PCs


# Task Requirements


# Configure Router-on-a-Stick as follows:

1. VLAN Networks
VLAN 10 = 192.168.10.0/24
VLAN 20 = 192.168.20.0/24
VLAN 30 = 192.168.30.0/24

2. Router Gateway Addresses

The router should use the last usable IP address in each subnet.

VLAN 10 → 192.168.10.254
VLAN 20 → 192.168.20.254
VLAN 30 → 192.168.30.254

3. Configure VLANs on the Switch

Assign the following PCs to VLANs:

PC1 → VLAN 10
PC2 → VLAN 20
PC3 → VLAN 30

4. Configure Trunk Link

Configure the port between the switch and router as a trunk port.

5. Configure Router Subinterfaces

Create router subinterfaces for each VLAN using 802.1Q encapsulation.

6. PC Addressing

PC1 = 192.168.10.10
PC2 = 192.168.20.10
PC3 = 192.168.30.10

7. Default Gateway
PC1 → 192.168.10.254
PC2 → 192.168.20.254
PC3 → 192.168.30.254
Verification

Verify connectivity between VLANs.

PC1 should be able to ping PC2
PC1 should be able to ping PC3
PC2 should be able to ping PC3

Successful pings confirm that Router-on-a-Stick is working correctly. 