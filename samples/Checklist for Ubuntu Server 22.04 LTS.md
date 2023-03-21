# Ubuntu Server 22.04 LTS - Cybersecurity and Hardening Checklist

## 1. Update and upgrade system packages

- Update the package list: `sudo apt-get update`
- Upgrade installed packages: `sudo apt-get upgrade`
- Remove unnecessary packages: `sudo apt-get autoremove`

## 2. Secure user accounts

- Set strong and unique passwords for all user accounts.
- Disable the root account: `sudo passwd -l root`
- Create a separate account with sudo privileges for administration tasks: `sudo adduser admin_user && sudo usermod -aG sudo admin_user`

## 3. Configure SSH for secure remote access

- Disable root login: In `/etc/ssh/sshd_config`, set `PermitRootLogin` to `no`
- Change the default SSH port: In `/etc/ssh/sshd_config`, change the `Port` number to a non-standard value
- Use public key authentication: Generate SSH keys for users and add the public keys to their `~/.ssh/authorized_keys` file
- Limit SSH access to specific users or groups: In `/etc/ssh/sshd_config`, use the `AllowUsers` or `AllowGroups` directives
- Configure idle session timeout: In `/etc/ssh/sshd_config`, set `ClientAliveInterval` and `ClientAliveCountMax` to appropriate values
- Disable empty passwords: In `/etc/ssh/sshd_config`, set `PermitEmptyPasswords` to `no`
- Disable X11 forwarding: In `/etc/ssh/sshd_config`, set `X11Forwarding` to `no`
- Restart the SSH service: `sudo systemctl restart ssh`

## 4. Configure and enable a firewall

- Install and enable UFW (Uncomplicated Firewall): `sudo apt-get install ufw && sudo ufw enable`
- Set default rules: `sudo ufw default deny incoming && sudo ufw default allow outgoing`
- Allow specific services and ports: `sudo ufw allow [service]` or `sudo ufw allow [port]/[protocol]`
- Limit incoming connections rate: `sudo ufw limit [port]/[protocol]`
- Enable logging: `sudo ufw logging on`

## 5. Harden the network configuration

- Disable IPv6 if not in use: In `/etc/sysctl.conf`, add `net.ipv6.conf.all.disable_ipv6 = 1`
- Enable SYN cookies protection: In `/etc/sysctl.conf`, add `net.ipv4.tcp_syncookies = 1`
- Enable IP spoofing protection: In `/etc/sysctl.conf`, add `net.ipv4.conf.default.rp_filter = 1`
- Apply the changes: `sudo sysctl -p`

## 6. Install and configure intrusion detection and prevention tools

- Install Fail2Ban: `sudo apt-get install fail2ban`
- Configure Fail2Ban by editing `/etc/fail2ban/jail.local` with appropriate settings
- Install and configure AIDE (Advanced Intrusion Detection Environment) or another intrusion detection tool

## 7. Regularly update and patch system software

- Schedule regular updates with a cron job or use unattended-upgrades
- Review and install security patches as needed

## 8. Install and configure antivirus software

- Install ClamAV: `sudo apt-get install clamav clamav-daemon`
- Update virus definitions: `sudo freshclam`
- Schedule regular scans with a cron job or use other tools for real-time scanning
