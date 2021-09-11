OpenWRT Config Files
=========

[![CI](https://github.com/pe-pe/ansible_role_openwrt_config_files/workflows/CI/badge.svg)](https://github.com/pe-pe/ansible_role_openwrt_config_files/actions)

Ansible role that copies files to OpenWRT device.

Requirements
------------
None

Role variables
--------------
Files to be copied to OpenWRT device are defined in `openwrt_config_files` variable (list of dictionary).
```yaml
openwrt_config_files:
  - { src: "wps_cancel.sh", dest: "/root/wps_cancel.sh", mode: "0755" }
  - { src: "wps_start.sh", dest: "/root/wps_start.sh", mode: "0755" }
```
If `openwrt_config_files` configuration variable is not present - no changes are made by role.

Dependencies
------------
This role depends on Ansible role `gekmihesg.openwrt` which allows to manage OpenWRT and derivatives with Ansible but without Python.

Example playbook using the role
-------------------------------
`./host_vars` \
`./host_vars/myrouter.yml`
```yaml
---
openwrt_config_files:
  - { src: "wps_cancel.sh", dest: "/root/wps_cancel.sh", mode: "0755" }
  - { src: "wps_start.sh", dest: "/root/wps_start.sh", mode: "0755" }
```
`./inventory.ini`
```ini
[openwrt]
myrouter
```
`./roles` \
`./roles/requirements.yml`
```yaml
---
roles:
- name: gekmihesg.openwrt
- name: pe_pe.openwrt_config_files
```
`./site.yml`
```yaml
---
- hosts: all
  roles:
    - role: gekmihesg.openwrt
    - role: pe_pe.openwrt_config_files
```
`./ansible.cfg`
```ini
[defaults]
# Define inventory location
inventory = ./inventory.ini
# Where to put roles downloaded from galaxy and other repos
roles_path = ./roles
# Defaults to /tmp to avoid flash wear on target device
remote_tmp = /tmp
```

Example execution
-----------------
Install roles and requirements:
```
ansible-galaxy role install -r roles/requirements.yml
```
Preview changes execution would perform on inventory:
```
ansible-playbook site.yml --check --diff
```
Execute playbook on inventory:
```
ansible-playbook site.yml
```
License
-------
MIT

Author Information
------------------
PePe
