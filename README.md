[![Build Status](https://img.shields.io/travis/ptavares/ansible-role-docker/master.svg?style=flat-square)](https://travis-ci.org/ptavares/ansible-role-docker)
[![Ansible Role](https://img.shields.io/ansible/role/29169.svg)](https://galaxy.ansible.com/ptavares/ansible-role-docker)
[![Ansible Role](https://img.shields.io/ansible/quality/29169.svg)](https://galaxy.ansible.com/ptavares/ansible-role-docker)
[![Ansible Role](https://img.shields.io/ansible/role/d/29169.svg)](https://galaxy.ansible.com/ptavares/ansible-role-docker)
[![License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](https://github.com/ptavares/ansible-role-docker/blob/master/LICENSE)

ansible-role-docker
=========

Ansible role for installating docker and docker-compose

Requirements
------------

Only test with ansible 2.5 min version

Role Variables
--------------
Available variables are listed below, along with default values (see [defaults/main.yml](https://github.com/ptavares/ansible-role-docker/blob/master/defaults/main.yml)):

### Docker options

```yaml
# Wanted Docker Edition - can be one of: 'ce' (Community Edition) or 'ee' (Enterprise Edition).
docker_edition: 'ce'
docker_package: "docker-{{ docker_edition }}"

# Install or remove docker_package : 'present' for install - 'absent' to uninstall
docker_package_state: present

# A list of users who will be added to the docker group (current user by default).
docker_users: []
```
### Docker service options

```yaml
# State : started - stopped
docker_service_state: started
# Enable service are boot or restart : yes / no
docker_service_enabled: yes
# Handler state for Docker service :
# - started : start the service if stopped
# - stopped : stop the service if started
# - restarted will always bounce the service
# - reloaded will always reload
docker_restart_handler_state: restarted
```
### Docker Compose options

```yaml
# Weather of not to install docker-compose
# Set to false if it's already installed and wanted to remove it
docker_compose_install: true
# Default to last version
# docker_compose_version: X.X.X
# Default path for docker-compose
docker_compose_path: /usr/local/bin/docker-compose
```

### Apt options

**Advanced user**

```yaml
# Avalaible channels :
# - stable
# - edge
# - nightly
docker_apt_release_channel: stable
# Url for apt key
docker_apt_key_url: https://download.docker.com/linux/{{ ansible_distribution|lower }}/gpg
# Docker apt repository url for amd64 arch
docker_apt_repository_url: "deb [arch=amd64] https://download.docker.com/linux/{{ ansible_distribution|lower }} {{ ansible_distribution_release }} {{ docker_apt_release_channel }}"
```

### Yum options

**Advanced user**

```yaml
# Url for gpg key
docker_gpg_key_url: https://download.docker.com/linux/centos/gpg
# Docker yum repository url for Fedora/CentOS/RHEL
docker_yum_repo_url: https://download.docker.com/linux/{{ (ansible_distribution == "Fedora") | ternary("fedora","centos") }}/docker-{{ docker_edition }}.repo
``` 

Dependencies
------------

No dependencie

Example Playbook
----------------

```yaml
- hosts: all
  roles:
    - role: ptavares.ansible_role_docker
```
Inside *`vars/main.yml`*:
- Copy content of [defaults/main.yml](https://github.com/ptavares/ansible-role-docker/blob/master/defaults/main.yml) in your playbook's vars file.
- Customize it as you like (filling role's variables)

License
-------

MIT
