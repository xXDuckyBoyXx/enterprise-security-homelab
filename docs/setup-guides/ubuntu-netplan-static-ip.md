# Ubuntu Server Static IP Configuration (Netplan + pfSense)

## Problem
Ubuntu Server repeatedly acquired a secondary DHCP address despite a static Netplan configuration.

## Root Cause
Cloud-init regenerated `/etc/netplan/50-cloud-init.yaml`, overriding static configuration at boot.

## Resolution
- Disabled cloud-init networking
- Removed cloud-managed Netplan file
- Enforced static routing with systemd-networkd
