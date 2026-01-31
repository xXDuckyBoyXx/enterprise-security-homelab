# Resolving Persistent DHCP on Ubuntu Server (cloud-init + Netplan)

## Symptoms
- Multiple IPv4 addresses on a single interface
- DHCP lease reappearing after reboot
- Dual default routes

## Investigation
- Verified Proxmox bridge assignment
- Confirmed Netplan syntax correctness
- Identified cloud-init override behavior

## Root Cause
cloud-init regenerated Netplan configuration at boot, re-enabling DHCP.

## Final Fix
- Disabled cloud-init networking
- Removed 50-cloud-init.yaml
- Rebooted to verify deterministic state
