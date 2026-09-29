# Routing Lab

A Cisco Packet Tracer lab focused on understanding basic network routing and communication between different IP networks.

## Objective

The goal of this lab is to understand how a router forwards packets between different networks using routing tables and static routes.

## Topology

The lab consists of:

* 2 Routers
* 2 PCs
* 3 network segments

```text
PC-A
192.168.10.10/24
     |
     |
R1
G0/0: 192.168.10.1/24
G0/1: 192.168.30.1/24
     |
     |
R2
G0/0: 192.168.30.2/24
G0/1: 192.168.20.1/24
     |
     |
PC-B
192.168.20.10/24
```

## IP Addressing

| Device | Interface | IP Address         | Network           |
| ------ | --------- | ------------------ | ----------------- |
| PC-A   | NIC       | `192.168.10.10/24` | `192.168.10.0/24` |
| R1     | G0/0      | `192.168.10.1/24`  | `192.168.10.0/24` |
| R1     | G0/1      | `192.168.30.1/24`  | `192.168.30.0/24` |
| R2     | G0/0      | `192.168.30.2/24`  | `192.168.30.0/24` |
| R2     | G0/1      | `192.168.20.1/24`  | `192.168.20.0/24` |
| PC-B   | NIC       | `192.168.20.10/24` | `192.168.20.0/24` |

## Routing

The two routers are directly connected through the `192.168.30.0/24` network.

However, R1 does not automatically know how to reach the `192.168.20.0/24` network behind R2.

A static route is therefore configured on R1:

```text
ip route 192.168.20.0 255.255.255.0 192.168.30.2
```

This tells R1:

> To reach `192.168.20.0/24`, forward the packet to R2 at `192.168.30.2`.

A return route is also required on R2 so that traffic can travel back to the `192.168.10.0/24` network.

## Testing

Connectivity is tested by sending ICMP traffic between the two end hosts.

```text
PC-A → R1 → R2 → PC-B
```

The important concept is that PC-A and PC-B belong to different IP networks. Communication between them therefore requires the routers to make forwarding decisions based on their routing tables.

## What I Learned

* How routers connect different IP networks
* How IP addressing relates to network boundaries
* How directly connected routes appear on a router
* Why a router needs a route to a remote network
* How static routes work
* Why routing requires a return path
* How to troubleshoot connectivity using `ping` and routing information

## Key Takeaway

Before moving into VLANs and other network services, I wanted to understand the basic mechanism behind routing first:

```text
Host
 ↓
Default Gateway
 ↓
Router
 ↓
Routing Table
 ↓
Next Hop
 ↓
Destination Network
```

This lab became the foundation for the next network lab, where the topology was expanded with VLANs, inter-VLAN routing, DHCP, DNS, and network segmentation.
