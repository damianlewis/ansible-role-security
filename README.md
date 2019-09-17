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
security_ssh_max_auth_retries: 2
```
Specifies the maximum number of authentication attempts permitted per connection.

```yaml
security_ssh_max_sessions: 10
```
Specifies the maximum number of open sessions permitted per network connection.

## Dependencies
None.

## Example Playbook
```yaml
- hosts: server
  become: yes

  vars:
    security_ssh_permit_root_login: yes
    security_ssh_password_authentication: yes

  tasks:
  - import_role:
      name: damianlewis.security
```

## License
MIT

## Author
Damian Lewis