# Ansible setup ufw role

> `ufw` is an [Ansible](http://www.ansible.com) role which:
>
> * installs ufw
> * configures ufw
> * configures ufw rules
> * configures service

## Dependencies

* Ansible >= 2.10

## Variables

Here is a list of all the default variables for this role, which are also available in `defaults/main.yml`.

```yaml
---
# Start the service and enable it on system boot
ufw_enabled: true

# List of packages to install
ufw_packages: ["ufw"]

# The service name
ufw_service: ufw

# List of rules to be applied
# see https://docs.ansible.com/ansible/latest/collections/community/general/ufw_module.html for documentation
ufw_rules:
  - rule: allow
    to_port: 22

# Manage the configuration file
ufw_manage_config: false

# Configuration object passed to the configuration file
ufw_config:
  IPV6: "yes"
  DEFAULT_INPUT_POLICY: DROP
  DEFAULT_OUTPUT_POLICY: ACCEPT
  DEFAULT_FORWARD_POLICY: DROP
  DEFAULT_APPLICATION_POLICY: SKIP
  MANAGE_BUILTINS: "no"
  IPT_SYSCTL: /etc/ufw/sysctl.conf
  IPT_MODULES: ""

# Path to the configuration file
ufw_config_file: /etc/default/ufw

```

## Handlers

These are the handlers that are defined in `handlers/main.yml`.

```yaml
---

- name: reset ufw
  community.general.ufw:
    state: reset

- name: reload ufw
  community.general.ufw:
    state: reloaded
  when: ufw_enabled | bool

```


## Usage

This is an example playbook:

```yaml
# @see https://docs.ansible.com/ansible/latest/collections/community/general/ufw_module.html#examples
---

- hosts: all
  become: true
  roles:
    - weareinteractive.ufw
  vars:
    ufw_rules:
      # Set loggin
      - logging: "full"
      # Allow OpenSSH
      - rule: allow
        name: OpenSSH
      # Delete OpenSSH rule
      - rule: allow
        name: OpenSSH
        delete: true
      # Allow all access to tcp port 80
      - rule: allow
        to_port: '80'
        proto: tcp
    # Manage the configuration file
    ufw_manage_config: true
    # Configuration object passed to the configuration file
    ufw_config:
      IPV6: "yes"
      DEFAULT_INPUT_POLICY: DROP
      DEFAULT_OUTPUT_POLICY: ACCEPT
      DEFAULT_FORWARD_POLICY: DROP
      DEFAULT_APPLICATION_POLICY: SKIP
      MANAGE_BUILTINS: "no"
      IPT_SYSCTL: /etc/ufw/sysctl.conf
      IPT_MODULES: ""

```

## License
Copyright (c) We Are Interactive under the MIT license.