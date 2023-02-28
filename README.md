# Introduction
Configurations for my wierd and potentially complicated systemd-networkd setups

# Devices
## rz5
Server setup based on re-purposed Ryzen 5 1600x PC
### NICs
 - Intel i211 1000 Mbps, pci-e 2.0 x1, onboard
 - Realtek rtl8125 2500 Mbps x4, pci-e 2.0 x4, pci-e AIC
### Setup
 - i211 and 1 of rtl8125's 4 ports bonded, connected to core switch as trunk, carrying vlan 7 and 17
 - the remaining 3 of rtl8125's 4 ports and the above bond combined as a bridge, carrying vlan 7, 17 and 25
 - 3 of the raw rtl8125 bridge slaves each connected to
   - 1 to nuc, carrying vlan 7 and 25
   - 1 to opi, carrying vlan 7 and 25
   - 1 to pc, carrying vlan 7, 17 and 25
### Addresses
 - 192.168.7.10 @ vlan7
 - 192.168.17.2 @ vlan17
 - 192.168.25.1 @ vlan25

## opi
SBC with RK3588S for native AArch64 builder and compilation works
### NICs
 - Rockchip 1000 Mbps MAC + YT8531 PHY, onboard
 - Realtek rtl8152 2500Mbps, usb 3.0
### Setup
 - 1G port connected to core switch, no vlan
 - 2.5G rtl8152 connected to rz5, carrying vlan 7 and 25
### Addresses
 - 192.168.7.11 @ vlan7
 - 192.168.7.251 @ vlan7
 - 192.168.25.11 @ vlan25

## nuc
SFF setup for lightweight workload
### NICs
 - Realtek rtl8111h 1000 Mbps, pci-e 1.1, onboard
 - Realtek rtl8125 2500Mbps, pci-e 2.0 x1, m.2 a+e card
### Setup
 - 1G port connected to core switch, no vlan
 - 2.5G rtl8152 connected to rz5, carrying vlan 7 and 25
### Addresses
 - 192.168.7.12 @ vlan7
 - 192.168.7.252 @ vlan7
 - 192.168.25.12 @ vlan25