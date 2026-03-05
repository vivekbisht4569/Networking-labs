## Introduction

Router-on-a-Stick (ROAS) is a networking technique used to enable communication between multiple VLANs using a single physical router interface. In this method, a trunk link is established between the switch and the router, allowing traffic from multiple VLANs to travel across the same connection.

The router uses logical interfaces called **subinterfaces**, where each subinterface is associated with a specific VLAN using **802.1Q encapsulation**. Each subinterface is assigned an IP address that acts as the **default gateway for devices in that VLAN**.

Router-on-a-Stick is commonly used in small or medium-sized networks where a Layer 3 switch is not available. It provides inter-VLAN routing without requiring multiple physical router interfaces.

