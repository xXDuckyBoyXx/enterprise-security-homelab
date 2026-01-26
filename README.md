# Enterprise-Security-Homelab
A segmented SOC-style homelab using Proxmox, pfSense, Wazuh SIEM, and Windows/Linux endpoints with detections mapped to MITRE ATT&amp;CK.

## **Overview**

This project is an enterprise-style security homelab designed to simulate a small SOC environment.
It focuses on network segmentation, endpoint visibility, SIEM alerting, and detection engineering using industry-relevant tools.

The lab is built to demonstrate real-world defensive security skills, including firewall policy design, log ingestion, alert tuning, and MITRE ATT&CK mapping.

## **What I Built**

* Virtualized security environment using Proxmox hosting pfSense, Wazuh (Manager, Indexer, Dashboard), Windows endpoints, and Ubuntu servers

* Implemented segmented virtual networking using Proxmox Linux bridges to separate WAN, LAN, and DMZ traffic routed through a virtualized pfSense firewall.

* Centralized security monitoring with endpoint telemetry, log collection, alerting, and dashboards via Wazuh

* Detection engineering and validation, including simulated attacks mapped to the MITRE ATT&CK framework

* Deployed pfSense CE in Proxmox using correct FreeBSD OS configuration, disk provisioning, and boot order, resolving UEFI/PXE boot failures.



