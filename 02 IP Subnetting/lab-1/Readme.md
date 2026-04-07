🛠️ What I Did

Divided 192.168.50.0/24 into 4 subnets (/26)

Connected 4 PCs to a multilayer switch

Assigned IP addresses to each subnet


Converted switch ports to Layer 3 using:
no switchport

Enabled routing:
ip routing

Verified connectivity using ping


🌐 IP Setup
PC0 → 192.168.50.10 → GW: 192.168.50.1

PC1 → 192.168.50.70 → GW: 192.168.50.65

PC2 → 192.168.50.130 → GW: 192.168.50.129

PC3 → 192.168.50.200 → GW: 192.168.50.193


📚 What I Learned

Subnetting (/24 → /26)

Default gateway concept

Multilayer switch can perform routing

Difference between Layer 2 and Layer 3 ports

Each interface must have a unique subnet


🚀 Result

All PCs in different subnets successfully communicated