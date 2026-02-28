# Static Routing
📌
# Definition

Static routing is a method where routes are manually configured on a router to reach specific destination networks. The router does not learn routes automatically. Each route must be defined by the network administrator.

 # ⚙ How It Works

1. When a packet arrives at the router:
2. The router checks its routing table.
3. If a static route matches the destination network,
4. The packet is forwarded to the configured next-hop IP address or exit interface.
5. There is no automatic exchange of routing information between routers.


# 📍 Where Static Routing Is Used

. Static routing is commonly used in:
. Small networks
. Stub networks (single exit path)
. Backup routes (floating static routes)
. Lab environments
. Secure networks requiring strict route control