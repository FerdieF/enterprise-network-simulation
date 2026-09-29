# VLAN & Network Services Simulation

A Cisco Packet Tracer homelab focused on building and troubleshooting a small segmented network.

This lab is a continuation of the basic routing lab. Instead of connecting separate networks through multiple routers, this lab explores how a single router can provide communication between multiple VLANs and network services.

## Objective

The main goal of this lab is to understand how VLANs, inter-VLAN routing, DHCP, DNS, and basic network segmentation work together in a small network environment.

## Network Design

The network is divided into three VLANs:

| VLAN | Name    | Network           | Purpose        |
| ---- | ------- | ----------------- | -------------- |
| 10   | USERS   | `192.168.10.0/24` | User devices   |
| 20   | SERVERS | `192.168.20.0/24` | Server devices |
| 30   | GUEST   | `192.168.30.0/24` | Guest devices  |

The router provides the default gateway for each VLAN through subinterfaces.

```text
                         Router
                    G0/0.10  .20  .30
                         |
                       TRUNK
                         |
                       Switch
              ┌──────────┼──────────┐
              │          │          │
           VLAN 10    VLAN 20    VLAN 30
           USERS      SERVERS      GUEST
              │          │          │
           PCs        Server       PC
```

## VLANs & Subnetting

Each VLAN is assigned its own IP subnet.

### VLAN 10 — Users

```text
Network:        192.168.10.0/24
Gateway:        192.168.10.1
```

### VLAN 20 — Servers

```text
Network:        192.168.20.0/24
Gateway:        192.168.20.1
```

### VLAN 30 — Guest

```text
Network:        192.168.30.0/24
Gateway:        192.168.30.1
```

Separating the VLANs provides logical separation between users, servers, and guest devices.

## Router-on-a-Stick

A trunk link connects the switch to the router.

The router uses subinterfaces to act as the default gateway for each VLAN:

```text
G0/0.10 → 192.168.10.1/24
G0/0.20 → 192.168.20.1/24
G0/0.30 → 192.168.30.1/24
```

Each subinterface is associated with its corresponding VLAN using IEEE 802.1Q encapsulation.

This allows the router to perform inter-VLAN routing.

## DHCP

DHCP is configured on the router to automatically provide IP configuration to devices in each VLAN.

The DHCP configuration provides:

* IP address
* Subnet mask
* Default gateway

Separate DHCP pools are configured for the three VLANs.

Infrastructure addresses can also be excluded from the DHCP range so that addresses such as the router gateway and server addresses remain available for static assignment.

## DNS

A server is configured in the Server VLAN with the address:

```text
192.168.20.10
```

DNS is used to resolve:

```text
server.local → 192.168.20.10
```

This demonstrates the difference between network connectivity and name resolution.

For example:

```text
ping 192.168.20.10
```

tests connectivity to the server's IP address.

While:

```text
ping server.local
```

also requires DNS resolution.

## Network Segmentation

The Guest VLAN is separated from the Users and Servers VLANs using an ACL.

The intended behavior is:

```text
Guest → Guest Gateway       Allowed
Guest → Users VLAN          Denied
Guest → Servers VLAN        Denied
```

This demonstrates how network segmentation can be combined with access control to restrict communication between different parts of a network.

## Troubleshooting

Troubleshooting was performed by intentionally changing configurations and observing the resulting behavior.

One example involved disabling the DNS service while keeping the server reachable by IP address.

The result:

```text
ping 192.168.20.10
        ↓
      Works

ping server.local
        ↓
      Fails
```

This helped distinguish between:

* Network connectivity
* IP addressing
* Routing
* DNS name resolution

The troubleshooting process generally follows:

```text
Interface
   ↓
IP Address
   ↓
ARP
   ↓
Routing
   ↓
ACL / Firewall
   ↓
Service
   ↓
Application
```

## What I Learned

Through this lab, I practiced:

* Creating and assigning VLANs
* Subnetting a network
* Configuring trunk links
* Configuring Router-on-a-Stick
* Performing inter-VLAN routing
* Configuring DHCP for multiple VLANs
* Using DHCP exclusions
* Configuring DNS
* Understanding IP address vs hostname resolution
* Applying ACLs for basic network segmentation
* Troubleshooting connectivity and network services

## Key Takeaway

This lab helped me understand that networking services are connected to each other.

A device having an IP address does not automatically mean that every service will work.

For example:

```text
DHCP
 ↓
IP Configuration
 ↓
Gateway
 ↓
Routing
 ↓
DNS
 ↓
Application / Service
```

Understanding these dependencies is important before moving into more advanced network security and monitoring labs.

## Disclaimer

This is a **personal learning homelab** created with Cisco Packet Tracer.

The topology and configurations are simulations for educational purposes and are not intended to represent a production network or production security configuration.
