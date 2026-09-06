# 🔐 Cisco Port Security Lab

## Overview
Configured and tested **Port Security** on a Cisco 2960 switch using Cisco Packet Tracer to prevent unauthorized devices from accessing the network through secured switch ports.

## Technologies
- Cisco Packet Tracer
- Cisco 2960 Switch
- Port Security
- Sticky MAC Address
- MAC Address Limiting
- Violation Mode

## Configuration
enable
configure terminal
interface fa0/1
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation restrict
end

## Verification
show port-security
show port-security interface fa0/1
show port-security address

## Key Takeaway
Port Security provides **Layer 2 security** by restricting which MAC addresses are allowed to communicate through a switch port and helps prevent unauthorized devices from gaining network access.