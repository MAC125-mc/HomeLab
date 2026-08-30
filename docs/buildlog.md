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
## Firewall Configuration
- Installed and enabled UFW.
- Set the default policy to deny incoming traffic and allow outgoing traffic.
- Allowed OpenSSH (TCP port 22) for remote administration.
- Verified SSH access still works after enabling the firewall.
## Nginx Web Server Deployment
- Installed Nginx
- Allowed HTTP traffic through UFW
- Enabled and started Nginx
- Verified Nginx is running by going to 192.168.56.101 (Host-Only IP)
- ## SSH Key Authentication and Hardening

* Generated an ED25519 SSH key pair on the Windows host:

  ```powershell
  ssh-keygen -t ed25519 -C "homelab-ubuntu"
  ```

* Added the Windows public key to the Ubuntu user's `~/.ssh/authorized_keys` file.

* Applied secure permissions:

  ```bash
  chmod 700 ~/.ssh
  chmod 600 ~/.ssh/authorized_keys
  ```

* Verified that SSH key-based login works from the Windows host without using the Ubuntu account password.

* Disabled password-based SSH authentication and root SSH login in:

  ```text
  /etc/ssh/sshd_config.d/99-hardening.conf
  ```

* Validated and reloaded the SSH service:

  ```bash
  sudo sshd -t
  sudo systemctl reload ssh
  ```

* Created a VirtualBox snapshot: `SSH Key Authentication and Hardening Complete`.

