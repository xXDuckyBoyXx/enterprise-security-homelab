#DHCP Lease Change Caused Loss of Access to Security Infrastructure

##Problem

After moving my Windows 10 workstation from the wireless router to a Netgear GS305 switch, I lost access to the pfSense and Wazuh dashboards. The workstation could no longer reach the pfSense LAN interface (192.168.10.1) or the Wazuh Manager (192.168.10.4).

##Symptoms

Windows workstation could not access:
pfSense Dashboard
Wazuh Dashboard
Initial ping tests failed.
Wazuh agent communication appeared disrupted.

##Investigation

I used several troubleshooting steps:

Verified the workstation's network configuration using:
