# ansible-role-system
Basic preparation for the operation system.

## Install

```shell
ansible-galaxy role install git+https://github.com/sergelogvinov/ansible-role-system.git,main
```

## Usage

```ini
# inventory file

[servers]
server-1          ansible_host=1.2.3.1
```

```yaml
# hosts/server-1.yaml

system_apt_auto_upgrade: true
system_sysctl:
  - { name: net.ipv4.ip_forward,          value: 1 }
  - { name: net.ipv6.conf.all.forwarding, value: 1 }
  - { name: net.ipv6.conf.all.autoconf,   value: 0 }
  - { name: net.ipv6.conf.all.accept_ra,  value: 0 }
system_network_hosts:
  - { ip: "{{ ansible_default_ipv4['address'] }}",    name: "{{ inventory_hostname }}{{ ' '+inventory_hostname.split('.')[0] if '.' in inventory_hostname }}" }

```

```yaml
# values.yaml

- hosts: servers
  roles:
    - ansible-role-system
```
