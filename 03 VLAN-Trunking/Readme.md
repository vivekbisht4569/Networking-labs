# VLAN & Trunking (Highly Important)

## Labs to Practice

1. Create VLAN 10 & VLAN 20
2. Assign switch ports to VLANs
3. Configure trunk between 2 switches
4. Verify isolation

## Important Concepts

- VLAN Segmentation
- 802.1Q
- Native VLAN

# VLAN & Trunking (Highly Important)

## Objective
To understand VLAN segmentation, configure VLANs on Cisco switches, assign switch ports to specific VLANs, establish trunk links between switches, and verify communication and isolation between VLANs.



## Important Concepts

### 1. VLAN Segmentation
A Virtual Local Area Network (VLAN) logically divides a physical Layer 2 network into separate broadcast domains.

**Benefits:**
- Improves network segmentation.
- Reduces unnecessary broadcast traffic.
- Helps isolate departments and devices.
- Supports better network administration and security.

### 2. IEEE 802.1Q
IEEE 802.1Q is the standard used to identify VLANs on Ethernet trunk links. It inserts a VLAN tag into Ethernet frames so the receiving switch can identify the appropriate VLAN.

### 3. Access Port
An access port normally carries traffic for a single VLAN and connects end devices such as PCs and printers.

### 4. Trunk Port
A trunk port carries traffic for multiple VLANs between switches or between a switch and a router.

### 5. Native VLAN
On an IEEE 802.1Q trunk, the native VLAN carries untagged traffic by default. Both ends of a trunk should have matching native VLAN configurations to avoid inconsistencies and potential security issues.

## Important Cisco Commands

```text
enable
configure terminal

vlan 10
 name SALES
exit

vlan 20
 name IT
exit

interface fa0/1
 switchport mode access
 switchport access vlan 10
exit

interface fa0/2
 switchport mode access
 switchport access vlan 20
exit

interface gi0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20
exit

end
show vlan brief
show interfaces trunk
show interfaces fa0/1 switchport
show running-config
```

**Note:** Interface names depend on the switch model. Configure the trunk on the actual inter-switch interface, and repeat the necessary VLAN and trunk configuration on the second switch.

## Expected Results
- VLAN 10 and VLAN 20 are created successfully.
- Switch ports are assigned to the correct VLANs.
- The trunk link transports traffic for both VLANs.
- Devices in the same VLAN can communicate across switches.
- Devices in different VLANs remain isolated until inter-VLAN routing is configured.

## What I Learned
- How VLANs divide a Layer 2 network into separate broadcast domains.
- How to configure access and trunk ports.
- How IEEE 802.1Q VLAN tagging works.
- Why native VLAN configuration matters.
- How to verify VLAN membership, trunk status, and network connectivity.

## Next Topic
**Inter-VLAN Routing → Router-on-a-Stick (ROAS)**

The next lab will demonstrate how a router enables communication between VLAN 10 and VLAN 20 using a trunk link and router subinterfaces.
