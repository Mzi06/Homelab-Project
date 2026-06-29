# Troubleshooting Log

A running record of real problems encountered while building this lab, and how they were diagnosed and resolved. Documenting this because troubleshooting is as much a part of the skill as the build itself.

---

### No internet access on fresh Ubuntu Server install
**Issue:** `apt update` failed with index file errors — server had no network connection at all.
**Diagnosis:** Server wasn't connected to any network yet; no DHCP, no manual config.
**Fix:** Temporarily connected via Ethernet, manually brought up the interface and assigned an IP/route using `ip link` and `ip route` commands, then set a working DNS resolver to get package installs working.

### Counterfeit USB-to-Serial console cable
**Issue:** Windows Device Manager flagged the console cable's chip as an unrecognized/counterfeit Prolific PL2303 chip, intermittently dropping the COM port connection.
**Diagnosis:** Confirmed faulty by testing on a second PC (Windows 11) — chip wasn't recognized there either.
**Fix:** Returned the cable under South Africa's Consumer Protection Act (Section 56) and replaced it with a working one.

### VM failed to start on Proxmox (QEMU exited with code 1)
**Issue:** New Windows Server VM failed to boot with a CPU feature error referencing missing AES instruction support.
**Diagnosis:** Host CPU didn't support the AES instruction set that Proxmox's default CPU type tried to expose to the VM.
**Fix:** Changed the VM's CPU type to `kvm64` for broader compatibility with older hardware.

### Forgotten Proxmox root password
**Issue:** Locked out of the Proxmox web interface after a typo or forgotten password during initial setup.
**Diagnosis:** No alternate admin account existed; needed local recovery access.
**Fix:** Recovered access via GRUB boot menu — edited the boot entry to load directly into a root shell (`init=/bin/bash`), remounted the filesystem as read-write, and reset the password with `passwd root`.

### IP address conflict between server and Windows PC
**Issue:** SSH connection refused despite the server and SSH service both appearing healthy.
**Diagnosis:** Windows PC and Ubuntu Server had both been assigned the same DHCP IP address, causing a conflict on the network.
**Fix:** Assigned the Ubuntu Server a fixed static IP via netplan to avoid future collisions.

### VLAN1 interface showing "up / line protocol down" on switch
**Issue:** Switch management IP was configured but unreachable via ping.
**Diagnosis:** No active connected ports on the switch — cables had been disconnected after a previous session.
**Fix:** Reconnected the router and server to the switch's physical ports; VLAN interface came up once an active link was present.
