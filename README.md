# Small Office Network Design and Configuration using Cisco Packet Tracer

## Project Overview

This project demonstrates the design, configuration, and verification of a small office network using Cisco Packet Tracer. Administration and IT devices are separated into different VLANs, and communication between the VLANs is enabled through router-on-a-stick inter-VLAN routing.

The project focuses on foundational networking skills relevant to entry-level Network Support and Network Engineering roles.

## Objectives

- Design a small office LAN in Cisco Packet Tracer
- Segment Administration and IT devices using VLANs
- Configure switch access ports and an IEEE 802.1Q trunk
- Configure router subinterfaces for inter-VLAN routing
- Configure DHCP pools to assign IPv4 settings automatically
- Verify gateway reachability and inter-VLAN connectivity using ICMP ping tests
- Practice basic network troubleshooting

## Network Topology

| Quantity | Device |
|---|---|
| 1 | Cisco 2911 router (R1) |
| 1 | Cisco 2960 switch (SW1) |
| 2 | Administration PCs (ADMIN-PC1, ADMIN-PC2) |
| 2 | IT PCs (IT-PC1, IT-PC2) |

**Logical layout:**

```
                 R1 (Router)
                      |
                802.1Q trunk
                      |
                 SW1 (Switch)
                /            \
     VLAN 10 - ADMIN      VLAN 20 - IT
       /         \          /        \
ADMIN-PC1   ADMIN-PC2   IT-PC1     IT-PC2
```

## IP Addressing Plan

| VLAN | Department | Network | Default Gateway |
|---|---|---|---|
| 10 | ADMIN | 192.168.10.0/24 | 192.168.10.1 |
| 20 | IT | 192.168.20.0/24 | 192.168.20.1 |

The PCs receive their IPv4 configuration through DHCP. The router gateway addresses are configured on router subinterfaces.

## Technologies and Concepts

- Cisco Packet Tracer
- Cisco IOS CLI
- VLANs (Virtual LANs)
- IEEE 802.1Q trunking
- DHCP (Dynamic Host Configuration Protocol)
- Router-on-a-stick
- Inter-VLAN routing
- IPv4 addressing and default gateways
- ICMP ping testing
- Basic troubleshooting and verification commands

## Configuration Summary

### VLANs and Switch Ports

- **VLAN 10:** ADMIN
- **VLAN 20:** IT
- End-device switch ports are configured as access ports in the appropriate VLAN.
- The switch-to-router link carries VLAN traffic over an 802.1Q trunk.

### Router Subinterfaces

| Subinterface | VLAN | Gateway |
|---|---|---|
| G0/0.10 | 10 | 192.168.10.1/24 |
| G0/0.20 | 20 | 192.168.20.1/24 |

### DHCP

DHCP pools are configured on the router to provide addresses to the ADMIN and IT networks. The exact leased addresses may vary depending on the Packet Tracer simulation.

## Verification and Test Results

| Test | Result |
|---|---|
| ADMIN-PC1 received an IPv4 address through DHCP | Passed |
| ADMIN-PC1 reached gateway 192.168.10.1 | Passed (4 sent, 4 received, 0% loss) |
| ADMIN-PC1 reached gateway 192.168.20.1 | Passed (4 sent, 4 received, 0% loss) |
| IT-PC2 reached gateway 192.168.20.1 | Passed (4 sent, 4 received, 0% loss) |
| IT-PC2 reached gateway 192.168.10.1 | Passed (4 sent, 4 received, 0% loss) |

These results confirm gateway reachability and routed connectivity between the two VLAN networks in the simulated environment. Initial ping latency can be higher while the simulation resolves addresses; the recorded tests completed with no packet loss.

## Useful Verification Commands

**On the switch (SW1):**

```
show vlan brief
show interfaces trunk
show mac address-table dynamic
```

**On the router (R1):**

```
show ip interface brief
show ip dhcp binding
show running-config
```

**On the PCs:**

```
ipconfig
ping 192.168.10.1
ping 192.168.20.1
```

## Troubleshooting Notes

During testing, one IT PC did not initially obtain an IPv4 address. The switch MAC address table showed that the PC was connected through `Fa0/5` in VLAN 1. The access port was then configured for VLAN 20, after which the PC obtained DHCP connectivity and gateway ping tests succeeded.

This demonstrates the importance of checking the actual switch port, VLAN assignment, DHCP lease, and gateway reachability rather than changing router settings without evidence.

## Skills Demonstrated

- Basic LAN design and device connectivity
- VLAN creation and port assignment
- Trunk configuration
- Router subinterface configuration
- DHCP configuration and lease verification
- Inter-VLAN connectivity testing
- CLI-based troubleshooting
- Technical documentation

## Project Files

```
small-office-network-cisco-packet-tracer/
├── README.md
├── small-office-network.pkt
└── screenshots/
    ├── network-topology.png
    ├── vlan-configuration.png
    ├── dhcp-verification.png
    └── connectivity-tests.png
```

## Limitations and Future Improvements

This is a foundational lab simulation, not a production-ready enterprise network. Possible future improvements:

- Add a dedicated server and test service connectivity
- Apply ACLs to control traffic between VLANs
- Add switch port security and unused-port shutdown
- Document a full port-to-device mapping and complete DHCP lease table

These improvements are not part of the currently verified implementation unless they are configured and tested separately.

## Author

Created as a networking portfolio project to practice Cisco Packet Tracer configuration, VLANs, DHCP, inter-VLAN routing, and troubleshooting.
