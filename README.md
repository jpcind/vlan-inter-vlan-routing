# VLAN & Inter-VLAN Routing Lab

## Overview

This project demonstrates VLAN segmentation and inter-VLAN routing using Cisco Packet Tracer.

The lab includes:

- Multiple VLANs on a Layer 2 switch
- Access port configuration
- 802.1Q trunking
- Router-on-a-stick
- Router subinterfaces
- Inter-VLAN routing
- Default gateway configuration
- Cisco IOS CLI verification and troubleshooting

## Network Design

The switch separates end devices into different VLANs.

Traffic between VLANs is forwarded to a router over a trunk link.

The router uses separate subinterfaces for each VLAN, allowing devices in different VLANs to communicate while remaining logically segmented at Layer 2.

## VLAN Configuration

The switch was configured with separate VLANs for different groups of hosts.

Access ports were assigned to the appropriate VLANs using Cisco IOS.

Example configuration:

```text
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# exit
