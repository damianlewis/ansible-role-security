# Ansible Role: Security
Server security configuration role.

## Requirements
None.

## Role Variables
Available variables are listed below, along with their default values.

```yaml
security_ssh_port: 22
```
The port on which SSH should listen. To prevent mis-configuring you should choose a port from the dynamic/private ports range: 49152-65535.

```yaml
security_ssh_permit_root_login: no
security_ssh_password_authentication: no
security_ssh_permit_empty_password: no
security_ssh_allow_agent_forwarding: no
security_ssh_allow_tcp_forwarding: no
security_ssh_tcp_keep_alive: no
security_ssh_use_dns: no
security_ssh_challenge_response_authentication: no
security_ssh_gss_api_authentication: no
security_ssh_x11_forwarding: no
```
Security settings for SSH. It's best to leave these set to false, however during initial server configuration when key-based authentication isn't configured, some of these settings can initially be set set to true.

```yaml
security_apt_periodic_update_package_list: 1
security_apt_periodic_download_upgradable_packages: 1
security_apt_periodic_autoclean: 7
security_apt_periodic_unattended_upgrades: 1
```
The APT::Periodic configuration settings.
- `security_apt_periodic_update_package_list:integer` - Update the apt packages cache every numnber of days.
- `security_apt_periodic_download_upgradable_packages:integer` - Downloading packages that can be upgraded every numnber of days.
- `security_apt_periodic_autoclean:integer` - Removing redundant packages using apt's 'autoclean' every numnber of days.
- `security_apt_periodic_unattended_upgrades:integer` - Install the available upgrades every numnber of days.

```yaml
security_unattended_upgrade_blacklist: []
security_unattended_upgrade_remove_unused_dependencies: no
security_unattended_upgrade_mail_to: ''
security_unattended_upgrade_mail_on_error: no
security_unattended_upgrade_reboot: no
security_unattended_upgrade_reboot_time: '02:00'
```
The Unattended-Upgrade configuration settings.
- `security_unattended_upgrade_blacklist:list` - A list of packages that will not be automatically upgraded.
- `security_unattended_upgrade_remove_unused_dependencies:boolean` - Specifies whether new unused dependencies should be removed after an upgrade (equivalent to apt-get autoremove).
- `security_unattended_upgrade_mail_to:string` - Send email to this address for problems or packages upgrades. If empty then no email is sent.
- `security_unattended_upgrade_mail_on_error:boolean` - Specifies whether emails should only be sent on errors. Default is to always send an email if `security_unattended_upgrade_mail_to` is set.
- `security_unattended_upgrade_reboot:boolean` - Specifies whether an automatic reboot should be performed after packages are upgraded.
- `security_unattended_upgrade_reboot_time:string` - If automatic reboot is enabled and needed, reboot at the specific time. Use the value 'now' to immediately reboot after upgrades.

## Dependencies
None.

## Example Playbook
```yaml
- hosts: server
  become: yes

  vars:
    security_ssh_permit_root_login: yes
    security_ssh_password_authentication: yes
    security_apt_periodic_autoclean: 21
    security_unattended_upgrade_blacklist:
    - vim
    - libc6
    security_unattended_upgrade_reboot_time: 'now'

  tasks:
  - import_role:
      name: damianlewis.security
```

## License
MIT

## Author
Damian Lewis