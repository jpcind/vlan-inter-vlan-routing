# VLAN & Inter-VLAN Routing Lab

## Overview

This Cisco Packet Tracer lab demonstrates VLAN segmentation, 802.1Q trunking, router-on-a-stick, and inter-VLAN routing.

The lab includes:

* Multiple VLANs on a Layer 2 switch
* Access port configuration
* 802.1Q trunking
* Router subinterfaces
* Router-on-a-stick
* Inter-VLAN routing
* Default gateway configuration
* Cisco IOS verification and troubleshooting

## Packet Tracer Lab File

The complete Cisco Packet Tracer lab is included in this repository:

`VLAN.pkt`

The file can be opened in Cisco Packet Tracer to inspect the VLAN configuration, trunk link, router subinterfaces, and inter-VLAN routing.

## Network Topology

The network uses a Layer 2 switch connected to end devices in separate VLANs.

A trunk link connects the switch to a router.

The router uses subinterfaces to route traffic between VLANs while allowing multiple VLANs to share one physical router interface.

![VLAN and Inter-VLAN Routing Topology](vlan%20topology.png)

## VLAN Configuration

Separate VLANs were created on the switch to logically segment devices.

Example:

```text
Switch> enable
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# exit
Switch(config)# vlan 20
Switch(config-vlan)# exit
```

Access ports were assigned to the appropriate VLANs.

Example:

```text
Switch(config)# interface fastEthernet0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
```

## Trunk Configuration

The switch port connected to the router was configured as a trunk.

Example:

```text
Switch> enable
Switch# configure terminal
Switch(config)# interface gigabitEthernet0/1
Switch(config-if)# switchport mode trunk
```

The trunk allows traffic from multiple VLANs to travel over one physical connection between the switch and router.

## Router-on-a-Stick

The router uses subinterfaces to provide Layer 3 routing for each VLAN.

Example:

```text
Router> enable
Router# configure terminal

Router(config)# interface gigabitEthernet0/0.10
Router(config-subif)# encapsulation dot1Q 10

Router(config)# interface gigabitEthernet0/0.20
Router(config-subif)# encapsulation dot1Q 20
```

Each subinterface is assigned an IPv4 address that acts as the default gateway for its VLAN.

The physical router interface is enabled with:

```text
Router(config)# interface gigabitEthernet0/0
Router(config-if)# no shutdown
```

## Inter-VLAN Routing

Devices within the same VLAN communicate through the Layer 2 switch.

When a device needs to communicate with a device in another VLAN, the traffic is sent to the router.

The traffic path is:

```text
Source Host
    ↓
Access Port
    ↓
Layer 2 Switch
    ↓
802.1Q Trunk
    ↓
Router Subinterface
    ↓
Inter-VLAN Routing
    ↓
Router Subinterface
    ↓
802.1Q Trunk
    ↓
Layer 2 Switch
    ↓
Destination Host
```

## Default Gateways

Each VLAN uses the IP address of its corresponding router subinterface as its default gateway.

This allows hosts to send traffic destined for another network to the router.

## Verification

The VLAN configuration can be verified with:

```text
Switch# show vlan brief
```

The trunk can be verified with:

```text
Switch# show interfaces trunk
```

The router subinterfaces can be verified with:

```text
Router# show ip interface brief
```

The complete device configurations can be inspected with:

```text
Switch# show running-config
Router# show running-config
```

Inter-VLAN connectivity is tested using `ping` between hosts in different VLANs.

## Technologies and Concepts

* Cisco Packet Tracer
* Cisco IOS CLI
* VLANs
* Access ports
* 802.1Q trunking
* Router-on-a-stick
* Router subinterfaces
* Inter-VLAN routing
* Default gateways
* IPv4 addressing
* Layer 2 switching
* Layer 3 routing
* Network troubleshooting

## Project Outcomes

* Created and configured multiple VLANs on a Cisco Layer 2 switch.
* Assigned switch access ports to specific VLANs.
* Configured an 802.1Q trunk between the switch and router.


## Verification Screenshots

### Inter-VLAN Connectivity

![Inter-VLAN Ping](screenshots/inter-vlan-ping.png)

### Additional Topology View

![Additional VLAN Topology](screenshots/my-top.png)

### Router-on-a-Stick Configuration

![Router-on-a-Stick Configuration](screenshots/router-on-a-stick-config.png)

### Router Subinterfaces

![Router Subinterfaces](screenshots/router-subinterfaces.png)

### Trunk Verification

![Show Interfaces Trunk](screenshots/show-interfaces-trunk.png)

### VLAN Membership

![Show VLAN Brief](screenshots/show-vlan-brief.png)

### Switch Access Port Configuration

![Switch Access Port Configuration](screenshots/switch-access-port-config.png)

### Switch Trunk Configuration

![Switch Trunk Configuration](screenshots/switch-trunk-config.png)

### VLAN Client IP Configuration

![VLAN Client IP Configuration](screenshots/vlan-client-ipconfig.png)

### Full VLAN Topology

![Full VLAN Topology](screenshots/vlan-topology.png)
