# FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| FABRIC | l3leaf | s1-brdr1 | 192.168.0.100/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s1-brdr2 | 192.168.0.101/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s1-leaf1 | 192.168.0.12/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s1-leaf2 | 192.168.0.13/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s1-leaf3 | 192.168.0.14/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s1-leaf4 | 192.168.0.15/24 | cEOSlab | Provisioned | - |
| FABRIC | spine | s1-spine1 | 192.168.0.10/24 | cEOSlab | Provisioned | - |
| FABRIC | spine | s1-spine2 | 192.168.0.11/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s2-brdr1 | 192.168.0.200/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s2-brdr2 | 192.168.0.201/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s2-leaf1 | 192.168.0.22/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s2-leaf2 | 192.168.0.23/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s2-leaf3 | 192.168.0.24/24 | cEOSlab | Provisioned | - |
| FABRIC | l3leaf | s2-leaf4 | 192.168.0.25/24 | cEOSlab | Provisioned | - |
| FABRIC | spine | s2-spine1 | 192.168.0.20/24 | cEOSlab | Provisioned | - |
| FABRIC | spine | s2-spine2 | 192.168.0.21/24 | cEOSlab | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | s1-brdr1 | Ethernet1 | mlag_peer | s1-brdr2 | Ethernet1 |
| l3leaf | s1-brdr1 | Ethernet2 | spine | s1-spine1 | Ethernet7 |
| l3leaf | s1-brdr1 | Ethernet3 | spine | s1-spine2 | Ethernet7 |
| l3leaf | s1-brdr1 | Ethernet4 | l3leaf | s2-brdr1 | Ethernet4 |
| l3leaf | s1-brdr1 | Ethernet6 | mlag_peer | s1-brdr2 | Ethernet6 |
| l3leaf | s1-brdr2 | Ethernet2 | spine | s1-spine1 | Ethernet8 |
| l3leaf | s1-brdr2 | Ethernet3 | spine | s1-spine2 | Ethernet8 |
| l3leaf | s1-brdr2 | Ethernet5 | l3leaf | s2-brdr2 | Ethernet5 |
| l3leaf | s1-leaf1 | Ethernet1 | mlag_peer | s1-leaf2 | Ethernet1 |
| l3leaf | s1-leaf1 | Ethernet2 | spine | s1-spine1 | Ethernet2 |
| l3leaf | s1-leaf1 | Ethernet3 | spine | s1-spine2 | Ethernet2 |
| l3leaf | s1-leaf1 | Ethernet6 | mlag_peer | s1-leaf2 | Ethernet6 |
| l3leaf | s1-leaf2 | Ethernet2 | spine | s1-spine1 | Ethernet3 |
| l3leaf | s1-leaf2 | Ethernet3 | spine | s1-spine2 | Ethernet3 |
| l3leaf | s1-leaf3 | Ethernet1 | mlag_peer | s1-leaf4 | Ethernet1 |
| l3leaf | s1-leaf3 | Ethernet2 | spine | s1-spine1 | Ethernet4 |
| l3leaf | s1-leaf3 | Ethernet3 | spine | s1-spine2 | Ethernet4 |
| l3leaf | s1-leaf3 | Ethernet6 | mlag_peer | s1-leaf4 | Ethernet6 |
| l3leaf | s1-leaf4 | Ethernet2 | spine | s1-spine1 | Ethernet5 |
| l3leaf | s1-leaf4 | Ethernet3 | spine | s1-spine2 | Ethernet5 |
| l3leaf | s2-brdr1 | Ethernet1 | mlag_peer | s2-brdr2 | Ethernet1 |
| l3leaf | s2-brdr1 | Ethernet2 | spine | s2-spine1 | Ethernet7 |
| l3leaf | s2-brdr1 | Ethernet3 | spine | s2-spine2 | Ethernet7 |
| l3leaf | s2-brdr1 | Ethernet6 | mlag_peer | s2-brdr2 | Ethernet6 |
| l3leaf | s2-brdr2 | Ethernet2 | spine | s2-spine1 | Ethernet8 |
| l3leaf | s2-brdr2 | Ethernet3 | spine | s2-spine2 | Ethernet8 |
| l3leaf | s2-leaf1 | Ethernet1 | mlag_peer | s2-leaf2 | Ethernet1 |
| l3leaf | s2-leaf1 | Ethernet2 | spine | s2-spine1 | Ethernet2 |
| l3leaf | s2-leaf1 | Ethernet3 | spine | s2-spine2 | Ethernet2 |
| l3leaf | s2-leaf1 | Ethernet6 | mlag_peer | s2-leaf2 | Ethernet6 |
| l3leaf | s2-leaf2 | Ethernet2 | spine | s2-spine1 | Ethernet3 |
| l3leaf | s2-leaf2 | Ethernet3 | spine | s2-spine2 | Ethernet3 |
| l3leaf | s2-leaf3 | Ethernet1 | mlag_peer | s2-leaf4 | Ethernet1 |
| l3leaf | s2-leaf3 | Ethernet2 | spine | s2-spine1 | Ethernet4 |
| l3leaf | s2-leaf3 | Ethernet3 | spine | s2-spine2 | Ethernet4 |
| l3leaf | s2-leaf3 | Ethernet6 | mlag_peer | s2-leaf4 | Ethernet6 |
| l3leaf | s2-leaf4 | Ethernet2 | spine | s2-spine1 | Ethernet5 |
| l3leaf | s2-leaf4 | Ethernet3 | spine | s2-spine2 | Ethernet5 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 10.0.0.0/24 | 256 | 48 | 18.75 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| s1-brdr1 | Ethernet2 | 10.0.0.17/31 | s1-spine1 | Ethernet7 | 10.0.0.16/31 |
| s1-brdr1 | Ethernet3 | 10.0.0.19/31 | s1-spine2 | Ethernet7 | 10.0.0.18/31 |
| s1-brdr1 | Ethernet4 | 10.255.0.0/31 | s2-brdr1 | Ethernet4 | 10.255.0.1/31 |
| s1-brdr2 | Ethernet2 | 10.0.0.21/31 | s1-spine1 | Ethernet8 | 10.0.0.20/31 |
| s1-brdr2 | Ethernet3 | 10.0.0.23/31 | s1-spine2 | Ethernet8 | 10.0.0.22/31 |
| s1-brdr2 | Ethernet5 | 10.255.0.2/31 | s2-brdr2 | Ethernet5 | 10.255.0.3/31 |
| s1-leaf1 | Ethernet2 | 10.0.0.1/31 | s1-spine1 | Ethernet2 | 10.0.0.0/31 |
| s1-leaf1 | Ethernet3 | 10.0.0.3/31 | s1-spine2 | Ethernet2 | 10.0.0.2/31 |
| s1-leaf2 | Ethernet2 | 10.0.0.5/31 | s1-spine1 | Ethernet3 | 10.0.0.4/31 |
| s1-leaf2 | Ethernet3 | 10.0.0.7/31 | s1-spine2 | Ethernet3 | 10.0.0.6/31 |
| s1-leaf3 | Ethernet2 | 10.0.0.9/31 | s1-spine1 | Ethernet4 | 10.0.0.8/31 |
| s1-leaf3 | Ethernet3 | 10.0.0.11/31 | s1-spine2 | Ethernet4 | 10.0.0.10/31 |
| s1-leaf4 | Ethernet2 | 10.0.0.13/31 | s1-spine1 | Ethernet5 | 10.0.0.12/31 |
| s1-leaf4 | Ethernet3 | 10.0.0.15/31 | s1-spine2 | Ethernet5 | 10.0.0.14/31 |
| s2-brdr1 | Ethernet2 | 10.0.0.17/31 | s2-spine1 | Ethernet7 | 10.0.0.16/31 |
| s2-brdr1 | Ethernet3 | 10.0.0.19/31 | s2-spine2 | Ethernet7 | 10.0.0.18/31 |
| s2-brdr2 | Ethernet2 | 10.0.0.21/31 | s2-spine1 | Ethernet8 | 10.0.0.20/31 |
| s2-brdr2 | Ethernet3 | 10.0.0.23/31 | s2-spine2 | Ethernet8 | 10.0.0.22/31 |
| s2-leaf1 | Ethernet2 | 10.0.0.1/31 | s2-spine1 | Ethernet2 | 10.0.0.0/31 |
| s2-leaf1 | Ethernet3 | 10.0.0.3/31 | s2-spine2 | Ethernet2 | 10.0.0.2/31 |
| s2-leaf2 | Ethernet2 | 10.0.0.5/31 | s2-spine1 | Ethernet3 | 10.0.0.4/31 |
| s2-leaf2 | Ethernet3 | 10.0.0.7/31 | s2-spine2 | Ethernet3 | 10.0.0.6/31 |
| s2-leaf3 | Ethernet2 | 10.0.0.9/31 | s2-spine1 | Ethernet4 | 10.0.0.8/31 |
| s2-leaf3 | Ethernet3 | 10.0.0.11/31 | s2-spine2 | Ethernet4 | 10.0.0.10/31 |
| s2-leaf4 | Ethernet2 | 10.0.0.13/31 | s2-spine1 | Ethernet5 | 10.0.0.12/31 |
| s2-leaf4 | Ethernet3 | 10.0.0.15/31 | s2-spine2 | Ethernet5 | 10.0.0.14/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 172.16.1.0/24 | 256 | 8 | 3.13 % |
| 172.16.2.0/24 | 256 | 8 | 3.13 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | s1-brdr1 | 172.16.1.7/32 |
| FABRIC | s1-brdr2 | 172.16.1.8/32 |
| FABRIC | s1-leaf1 | 172.16.1.3/32 |
| FABRIC | s1-leaf2 | 172.16.1.4/32 |
| FABRIC | s1-leaf3 | 172.16.1.5/32 |
| FABRIC | s1-leaf4 | 172.16.1.6/32 |
| FABRIC | s1-spine1 | 172.16.1.1/32 |
| FABRIC | s1-spine2 | 172.16.1.2/32 |
| FABRIC | s2-brdr1 | 172.16.2.7/32 |
| FABRIC | s2-brdr2 | 172.16.2.8/32 |
| FABRIC | s2-leaf1 | 172.16.2.3/32 |
| FABRIC | s2-leaf2 | 172.16.2.4/32 |
| FABRIC | s2-leaf3 | 172.16.2.5/32 |
| FABRIC | s2-leaf4 | 172.16.2.6/32 |
| FABRIC | s2-spine1 | 172.16.2.1/32 |
| FABRIC | s2-spine2 | 172.16.2.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 172.16.100.0/24 | 256 | 6 | 2.35 % |
| 172.16.200.0/24 | 256 | 6 | 2.35 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| FABRIC | s1-brdr1 | 172.16.100.7/32 |
| FABRIC | s1-brdr2 | 172.16.100.7/32 |
| FABRIC | s1-leaf1 | 172.16.100.3/32 |
| FABRIC | s1-leaf2 | 172.16.100.3/32 |
| FABRIC | s1-leaf3 | 172.16.100.5/32 |
| FABRIC | s1-leaf4 | 172.16.100.5/32 |
| FABRIC | s2-brdr1 | 172.16.200.7/32 |
| FABRIC | s2-brdr2 | 172.16.200.7/32 |
| FABRIC | s2-leaf1 | 172.16.200.3/32 |
| FABRIC | s2-leaf2 | 172.16.200.3/32 |
| FABRIC | s2-leaf3 | 172.16.200.5/32 |
| FABRIC | s2-leaf4 | 172.16.200.5/32 |
