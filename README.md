# Enterprise Network Simulation

A personal homelab project built with **Cisco Packet Tracer** as part of my learning journey in networking and cybersecurity.

This repository documents my hands-on practice with building, configuring, and troubleshooting small network environments. The goal is not to create a production-ready network, but to understand how networking concepts work in practice.

## About This Homelab

I started this project to strengthen my networking fundamentals before going deeper into cybersecurity.

Rather than only learning concepts theoretically, I use Cisco Packet Tracer to build small networks and troubleshoot problems myself.

The labs gradually introduce concepts such as:

* IP addressing
* Subnetting
* Routing
* Static routes
* VLANs
* Router-on-a-Stick
* DHCP
* DNS
* Network segmentation
* Access Control Lists (ACLs)
* Network troubleshooting

## Projects

### 01 — Routing

A basic routing lab focused on communication between different IP networks using routers and static routes.

See [`routing/`](./routing/).

### 02 — VLAN & Network Services

An expanded network lab introducing VLANs, inter-VLAN routing, DHCP, DNS, network segmentation, and troubleshooting.

See [`vlan-and-network-services/`](./vlan-and-network-services/).

## Learning Approach

The main purpose of this homelab is to understand **why** a network works, not just memorize commands.

When troubleshooting, I try to follow the path from the lower layers upward:

```text
Physical / Virtual Layer
        ↓
Interface
        ↓
IP Address
        ↓
ARP
        ↓
Routing
        ↓
Firewall / ACL
        ↓
Service
        ↓
Application
```

Each lab is documented based on what I actually built and learned while working through the topology.

## Tools

* Cisco Packet Tracer
* Git / GitHub

## Disclaimer

This is a **personal learning homelab**.

The configurations and topologies in this repository are simulations created for educational purposes. They are not intended to represent production network architectures or production security configurations.

The purpose of this repository is to document my learning process, experiments, troubleshooting, and growing understanding of networking fundamentals.
