# Ansible Role: RHEL 9.3 Base Configuration

This Ansible role provides a comprehensive base configuration for Red Hat Enterprise Linux 9.3 servers. It includes tasks for system setup, network configuration, package management, and integration with various services like Red Hat, Proxmox, and Tailscale.

## Requirements
------------

- Ansible 2.14 or higher
- Red Hat Enterprise Linux 9.3 target systems
- Valid Red Hat subscription
- Proxmox API access
- Tailscale account (if using Tailscale VPN)

## Role Variables
--------------

#### Red Hat Subscription Manager

```
redhat_secrets:
  username: "your_redhat_username"
  password: "your_redhat_password"
```

#### Tailscale
```
ts_secrets:
  authkey: "your_tailscale_authkey"
```

#### Proxmox
```
proxmox_secrets:
  api:
    token_secret: "your_proxmox_api_token_secret"
  ci:
    password: "your_proxmox_ci_password"
```

## Usage
--------------
Include this role in your playbook.
Customize the variables as needed, particularly the secret variables.
Run your playbook.

## Example Playbook
--------------
```
- hosts: servers
  roles:
    - role: rhel-9.3-base
      vars:
        redhat_secrets:
          username: "{{ lookup('env', 'REDHAT_USERNAME') }}"
          password: "{{ lookup('env', 'REDHAT_PASSWORD') }}"
        ts_secrets:
          authkey: "{{ lookup('env', 'TS_AUTHKEY') }}"
        proxmox_secrets:
          api:
            token_secret: "{{ lookup('env', 'PROXMOX_API_TOKEN_SECRET') }}"
          ci:
            password: "{{ lookup('env', 'PROXMOX_CI_PASSWORD') }}"
```

## Role Structure
--------------
```
rhel-9.3-base/
├── defaults/
│   └── main.yml
├── handlers/
│   └── main.yml
├── tasks/
│   ├── main.yml
│   └── ...
├── templates/
│   └── ...
├── vars/
│   ├── main.yml
│   └── secrets.yml
├── tests/
│   └── ...
└── README.md
```