Role Name
=========

An [Ansible] role to provision a [Docker] swarm cluster.

Requirements
------------

Install [Ansible] roles required:

```
sudo ansible-galaxy install -r requirements.yml
```

Role Variables
--------------

```
---
# defaults file for ansible-docker-swarm
docker_swarm_addr: "{{ hostvars[inventory_hostname]['ansible_' + docker_swarm_interface]['ipv4']['address'] }}"

# Validity period for node certificates (default 2160h0m0s)
docker_swarm_cert_expiry: '2160h0m0s'

# Dispatcher heartbeat period (default 5s)
docker_swarm_dispatcher_heartbeat_duration: '5s'

docker_swarm_interface: "enp0s8"
# docker_swarm_managers_ansible_group: 'docker-swarm-managers'

docker_swarm_config_networks: false
docker_swarm_config_settings: false

# Define Ansible group which contains your Docker swarm managers
docker_swarm_managers_ansible_group: 'docker-swarm-managers'

docker_swarm_networks: []
  # - name: 'my_net'
  #   driver: 'overlay'
  #   state: 'present'
  # - name: 'test'
  #   driver: 'overlay'
  #   state: 'absent'
docker_swarm_port: "2377"

# Defines first node in docker_swarm_managers_ansible_group as primary
docker_swarm_primary_manager: '{{ groups[docker_swarm_managers_ansible_group][0] }}'

# Task history retention limit (default 5)
docker_swarm_task_history_limit: '5'

# Define Ansible group which contains you Docker swarm workers
docker_swarm_workers_ansible_group: 'docker-swarm-workers'
```

Dependencies
------------

None

Example Playbook
----------------

```
- hosts: docker_hosts
  become: true
  vars:
  roles:
    - role: ansible-docker
    - role: ansible-docker-swarm
  tasks:
```

## Дополнительно [psyd01986]

```
Добавил поддержку Ubuntu 20.04
```


License
-------

BSD

Author Information
------------------

Larry Smith Jr.

- @mrlesmithjr
- http://everythingshouldbevirtual.com
- mrlesmithjr [at] gmail.com
