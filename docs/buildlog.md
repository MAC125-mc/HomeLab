# Build Log

## 2026-08-30 — Ubuntu Server VM created
- Installed Oracle VirtualBox
- Created Ubuntu Server virtual machine
- Assigned 2 CPU cores, 4 GB RAM, and 30 GB storage
- Turned on geographical location
## Network Verification
- Configured Adapter 1 as NAT in VirtualBox.
- Confirmed outbound connectivity with:
  `ping -c 4 8.8.8.8`
  ## Base Server Configuration
- Updated Ubuntu packages.
- Installed OpenSSH Server, curl, and net-tools.
- Verified the SSH service is active.
- Recorded the VM network configuration with `ip addr`.
- Created a VirtualBox snapshot: “Ubuntu Server – Base Configuration Complete.”
## Private Management Network and SSH
- Retained NAT on Adapter 1 for internet access.
- Added a Host-Only Adapter as Adapter 2 for private host-to-VM communication.
- Identified the VM’s Host-Only IP address with `ip -br addr`.
- Connected from the Windows host using SSH.
- ## Firewall Configuration
- Installed and enabled UFW.
- Set the default policy to deny incoming traffic and allow outgoing traffic.
- Allowed OpenSSH (TCP port 22) for remote administration.
- Verified SSH access still works after enabling the firewall.
