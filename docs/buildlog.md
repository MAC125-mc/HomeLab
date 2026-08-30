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
