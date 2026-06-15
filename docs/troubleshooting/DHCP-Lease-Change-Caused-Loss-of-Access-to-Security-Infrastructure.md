# DHCP Lease Change Caused Loss of Access to Security Infrastructure

## Problem

After moving my Windows 10 workstation from the wireless router to a Netgear GS305 switch, I lost access to the pfSense and Wazuh dashboards. The workstation could no longer reach the pfSense LAN interface (192.168.10.1) or the Wazuh Manager (192.168.10.4).

## Symptoms

Windows workstation could not access:
- pfSense Dashboard
- Wazuh Dashboard
- Initial ping tests failed.
- Wazuh agent communication appeared disrupted.

## Investigation

I used several troubleshooting steps:

- Verified the workstation's network configuration using:
>```cmd
>`ipconfig`
- Discovered the Windows workstation's DHCP-assigned IP address had changed:

| Before        | After         |
| ------------- | ------------- |
| 192.168.xxx.xxx | 192.168.xxx.xxx |

- Confirmed Proxmox remained reachable.
- Reviewed pfSense firewall aliases and discovered that access rules only permitted the original workstation IP address.

## Root Cause

Firewall aliases were configured using a specific DHCP-assigned IP address. When the workstation received a new lease after being moved to the switch, it no longer matched the allowed source address.

## Resolution

- Updated pfSense firewall aliases to include the workstation's new IP address.
- Applied the updated firewall rules.
- Verified connectivity using ping tests.
- Restored access to both dashboards.
- Confirmed Wazuh agent connectivity resumed without requiring agent reinstallation.

## Lessons Learned

- Avoid using dynamic DHCP addresses in security firewall rules.
- Implement static DHCP reservations for administrative workstations.
- Validate routing and firewall policies after physical network changes.
- Troubleshooting and documentation are as important as initial deployment.
