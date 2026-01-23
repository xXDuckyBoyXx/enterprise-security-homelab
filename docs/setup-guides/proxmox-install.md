# Proxmox VE Installation Guide

## Overview

This document details the installation and initial configuration of **Proxmox Virtual Environment (VE)** as the foundational hypervisor for an enterprise-style security homelab. Proxmox was selected to provide a stable, always-on virtualization platform capable of hosting firewall, SIEM, and endpoint systems in a segmented network architecture.

---

## Why Proxmox VE?

Proxmox VE is an open-source, enterprise-grade virtualization platform built on Debian Linux. It provides:

- Type-1 (bare-metal) hypervisor architecture
- Native support for KVM virtual machines and LXC containers
- Advanced networking (bridges, VLANs, multiple NICs)
- Web-based management interface
- Snapshotting, backups, and role-based access control

This makes it ideal for simulating real-world infrastructure used in enterprise and security-focused environments.

---

## Hardware Requirements

**Minimum Requirements**
- 64-bit CPU with virtualization support (Intel VT-x / AMD-V)
- 8 GB RAM (16 GB+ recommended)
- 1 storage device (SSD strongly recommended)
- At least 1 network interface

**Recommended (Lab Environment)**
- Multi-core CPU (4+ cores)
- 32 GB RAM
- Dedicated SSD or NVMe for VM storage
- Multiple NICs for WAN/LAN/DMZ segmentation

---

## BIOS / UEFI Configuration

Before installing Proxmox, the following BIOS/UEFI settings must be verified:

- **Virtualization Technology**: Enabled  
  - Intel: VT-x / VT-d  
  - AMD: SVM / IOMMU
- **Secure Boot**: Disabled
- **Boot Mode**: UEFI (preferred)
- **Fast Boot**: Disabled (recommended for troubleshooting)

> Validation Tip:  
> From a Linux live environment, confirm virtualization support:
> ```bash
> lscpu | grep Virtualization
> ```

---

## Installation Media Preparation

1. Download the latest Proxmox VE ISO from:
   - https://www.proxmox.com/en/downloads

2. Create a bootable USB using one of the following:
   - Rufus (Windows)
   - Balena Etcher (cross-platform)
   - `dd` (Linux/macOS)

---

## Proxmox VE Installation Steps

1. Boot the system from the Proxmox USB installer
2. Select **Install Proxmox VE**
3. Accept the license agreement
4. Select the target disk  
   - Default LVM configuration used for this lab
5. Configure:
   - Country / Time Zone / Keyboard Layout
6. Set:
   - Root password
   - Administrative email address
7. Configure network settings:
   - Management IP (static recommended)
   - Hostname (FQDN format)
   - Default gateway
   - DNS server

8. Confirm settings and begin installation

Installation typically completes within 5–10 minutes.

---

## Post-Installation Access

After installation completes, access the Proxmox web interface from another machine:

https://<**proxmox-ip>**:8006

Log in with:
- **Username:** root
- **Realm:** PAM
- **Password:** (set during installation)

---

## Initial Post-Install Configuration

### Update System Packages

```bash
apt update && apt full-upgrade -y


