# Initial setup on Debian

To get started with Docker Engine on Debian, make sure you meet the prerequisites, then install Docker.

## Pre-requisites

* You must have [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) installed on your computer.

# OS requirements
To install Docker Engine, you need the 64-bit version of one of these Debian.

## Quick start

Config the host with Ansible:

Ansible code one that deploys everything you need to run service - docker and related.
```shell
git clone https://github.com/DenAV/ansible-host-initial-setting.git

cd ansible-host-initial-setting
ansible-playbook playbooks/pl_initial_setting_local.yml -bK

or 

sudo ansible-playbook playbooks/pl_initial_setting_local.yml
```
