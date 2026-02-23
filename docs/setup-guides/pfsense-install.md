# pfSense Installation Procedure (Proxmox Homelab)

## Purpose

This document provides a **step-by-step installation procedure** for deploying **pfSense** as the primary firewall and network segmentation device in an **Enterprise Security Homelab** running on **Proxmox VE**.

The goal of this setup is to simulate a **real-world firewall deployment** while remaining safe, reproducible, and portfolio-ready.

---

## Scope

This guide covers:

* |pfSense installation as a virtual machine on Proxmox |
* |Initial interface assignment                         |
* |Basic network configuration                          |
* |Web dashboard access                                 |

> All IP addresses, hostnames, and identifiers referenced here are **examples only**. 

---

## Prerequisites

* Proxmox VE installed and accessible
* pfSense ISO downloaded (Community Edition)
* At least **two Proxmox network bridges** configured:

  * WAN bridge (internet-facing)
  * LAN bridge (internal network)

### Recommended VM Resources

| Resource | Value         |
| -------- | ------------- |
| vCPU     | 2             |
| RAM      | 2–4 GB        |
| Storage  | 16–32 GB      |
| NICs     | 2 (WAN + LAN) |

---

## Step 1 – Upload pfSense ISO to Proxmox

1. Log into the Proxmox web interface
2. Navigate to **Datacenter → Storage → ISO Images**
3. Upload the pfSense ISO file

---

## Step 2 – Create the pfSense Virtual Machine

1. Click **Create VM**
2. Assign:

   * **Name:** `pfsense-fw`
   * **OS:** Use uploaded pfSense ISO
3. System:

   * BIOS: Default (SeaBIOS)
   * Machine: Default
4. Disks:

   * Bus/Device: VirtIO
   * Size: 16–32 GB
5. CPU:

   * Cores: 2
6. Memory:

   * 2048–4096 MB
7. Network:

   * **NIC 1:** WAN bridge (VirtIO)
   * **NIC 2:** LAN bridge (VirtIO)
8. Finish VM creation

---

## Step 3 – Install pfSense

1. Start the pfSense VM
2. Open the console
3. Select:

   * **Install pfSense**
   * Keymap: Default
   * Partitioning: Auto (ZFS or UFS)
4. Confirm installation and reboot when complete
5. Remove ISO after installation

---

## Step 4 – Interface Assignment

Upon first boot:

1. When prompted to assign interfaces:

   * Identify **WAN** and **LAN** based on MAC address order
2. Assign:

   * `em0` (or vtnet0) → WAN
   * `em1` (or vtnet1) → LAN
3. Enable webConfigurator on LAN

---

## Step 5 – Initial Network Configuration

From the pfSense console menu:

* WAN:

  * Typically DHCP (via ISP router)
* LAN:

  * Static IP (example): `192.168.10.1/24`
  * DHCP Server: Enabled

> These values may differ depending on your lab design.

---

## Step 6 – Access pfSense Web Dashboard

1. From a LAN-connected device, browse to:

   ```
   https://192.168.10.1
   ```
2. Accept the security warning
3. Log in with default credentials:

   * Username: `admin`
   * Password: `pfsense`

---

## Step 7 – Initial Setup Wizard

Complete the pfSense setup wizard:

* Hostname and domain (lab-specific)
* DNS servers
* Time zone
* WAN configuration
* Change **admin password**

---

## Validation Checklist

* pfSense dashboard accessible from LAN
* WAN interface has IP address
* LAN clients receive DHCP leases
* Internet access confirmed from LAN

---

## Security Notes

* Default deny rules are enforced on WAN
* LAN → WAN traffic permitted by default
* Admin access restricted to LAN

Future hardening steps include:

* Firewall rule tightening
* VLAN creation
* Management network isolation

---

## Next Steps

* Create additional interfaces or VLANs
* Deploy Wazuh SIEM behind pfSense
* Implement DMZ segmentation
* Add logging and alerting
