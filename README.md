# Homelab Project

A self-built home lab documenting my hands-on journey from networking fundamentals to enterprise infrastructure — built piece by piece while working toward a career in IT support, networking, and eventually cloud security.

## Goal

I'm CompTIA Security+ certified and building practical, hands-on skills to complement it. This lab simulates a small enterprise network and directory environment, the kind of setup you'd find in a real IT support or junior sysadmin role, so I can develop and demonstrate real troubleshooting and infrastructure skills rather than just theory.

## Hardware

- **Switch:** Cisco Catalyst 3560 (managed, configured via Cisco IOS)
- **Router:** TP-Link AC750 Dual Band
- **Server:** Repurposed PC running Proxmox VE (bare-metal hypervisor)

## Network Topology

```
[Internet/ISP] 
      |
  [TP-Link Router] (192.168.0.1)
      |
  [Cisco Catalyst 3560 Switch] (192.168.0.2)
      |
      ├── [Proxmox Host] (192.168.0.10)
      |        └── [Windows Server 2022 VM] (192.168.0.101) — AD DC + DNS
      |
      └── [Ubuntu Server] (192.168.0.50)
```

## What's Built So Far

### 1. Network Foundation
- Configured the Cisco Catalyst 3560 from scratch via console connection (hostname, enable/VTY passwords, management VLAN interface)
- Set static IP addressing across all core devices
- Verified end-to-end connectivity between router, switch, and servers

### 2. Server & Remote Access
- Deployed Ubuntu Server, configured networking manually via Linux CLI (netplan, `ip` commands)
- Set up and hardened SSH for remote administration

### 3. Virtualization Layer
- Installed Proxmox VE as a dedicated bare-metal hypervisor
- Resolved a CPU compatibility issue (missing AES instruction support) by adjusting the VM's CPU type
- Deployed a Windows Server 2022 VM

### 4. Active Directory Environment
- Promoted the Windows Server VM to a full Active Directory Domain Controller (`homelab.local`)
- Built out Organizational Units (IT, Sales, HR) reflecting a real departmental structure
- Created test user accounts and assigned them to their respective OUs
- Created Security Groups (IT-Admins, Sales-Team, HR-Team) for role-based access
- Configured a Group Policy Object enforcing password complexity and minimum length on the IT OU

## In Progress / Next Up

- VLAN segmentation on the Cisco switch, tying network segmentation back to the AD department structure
- Joining a client VM to the domain
- Exploring SIEM tooling (e.g. Wazuh) for log monitoring and detection

## Troubleshooting Log

A real record of problems hit along the way and how they were resolved — see [`troubleshooting-log.md`](./troubleshooting-log.md).

## Notes

All IP addresses shown are private/local addresses used within an isolated home lab network. No real organizational data is used anywhere in this project — all users, groups, and structures are fictional examples for learning purposes.
