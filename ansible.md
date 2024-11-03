# ansible

## Installation

```sh
pipx install --include-deps ansible
```

## inventory

```sh
ansible-inventory --list -i inventory.ini
```

if you don't want to use keys then password is required, add the following to inventory.ini

also `sshpass` is required

```ini
[all:vars]
ansible_password=<password>
```

## Run playbook

Example of playbook

`update.yml`
```yaml
- name: Update system packages
  hosts: webservers
  become: true
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes
        cache_valid_time: 3600
    - name: Upgrade all packages
      apt:
        upgrade: dist
    - name: Remove unused packages
      apt:
        autoremove: yes
```

```sh
ansible-playbook update.yml -i inventory.ini
```