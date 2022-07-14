# [mongodb](#mongodb)

|GitHub|GitLab|
|------|------|
|[![github](https://github.com/mullholland/ansible-role-mongodb/workflows/Ansible%20Molecule/badge.svg)](https://github.com/mullholland/ansible-role-mongodb/actions)|[![gitlab](https://gitlab.com/mullholland/ansible-role-mongodb/badges/master/pipeline.svg)](https://gitlab.com/mullholland/ansible-role-mongodb)|[![quality](https://img.shields.io/ansible/quality/unset)](https://galaxy.ansible.com/mullholland/mongodb)|

description

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
mongodb_yum_repository:
  name: "mongodb-org-5.0"
  baseurl: "https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/5.0/x86_64/"
  gpgcheck: "1"
  gpgkey: "https://www.mongodb.org/static/pgp/server-5.0.asc"
  enabled: "1"

mongodb_apt_repository:
  name: "mongodb-org-5.0"
  gpgkey: "https://www.mongodb.org/static/pgp/server-5.0.asc"
  repo: 'deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/{{ ansible_distribution | lower }} {{ ansible_distribution_release | lower }}/mongodb-org/5.0 {{ "multiverse" if ansible_distribution == "Ubuntu" else "main" }}'

mongodb_packages:
  - "mongodb-org"

mongodb_packages_pin: false

# To pin the mongodb version install a specifiv versions
# and enable pin
# mongodb_packages:
#   - "mongodb-org-5.0.9"
#   - "mongodb-org-database-5.0.9"
#   - "mongodb-org-server-5.0.9"
#   - "mongodb-org-shell-5.0.9"
#   - "mongodb-org-mongos-5.0.9"
#   - "mongodb-org-tools-5.0.9"
# mongodb_packages_pin: true

# for documentation of all options, see:
#   http://docs.mongodb.org/manual/reference/configuration-options/
# Will be writenn with `to_nice_yaml` to {{ mongodb_config_file }}
mongodb_config:
  storage:
    dbPath: "{{ mongodb_data_dir }}"
    journal:
      enabled: true
  systemLog:
    destination: file
    logAppend: true
    path: "{{ mongodb_log_dir }}/mongod.log"
  net:
    port: 27017
    bindIp: 127.0.0.1
  processManagement:
    timeZoneInfo: /usr/share/zoneinfo

# Log rotation
mongodb_logrotate: true
mongodb_logrotate_options:
  - compress
  - copytruncate
  - daily
  - dateext
  - rotate 7
```


## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true
  # vars:
  #   example_var: "value"
  roles:
    - role: "mullholland.mongodb"
```





## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

-   [debian10](https://hub.docker.com/r/mullholland/docker-molecule-debian10)
-   [debian11](https://hub.docker.com/r/mullholland/docker-molecule-debian11)
-   [ubuntu1804](https://hub.docker.com/r/mullholland/docker-molecule-ubuntu1804)
-   [ubuntu2004](https://hub.docker.com/r/mullholland/docker-molecule-ubuntu2004)

The minimum version of Ansible required is 2.10, tests have been done to:

-   The previous versions.
-   The current version.
-   The [devel](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-devel-from-github-with-pip) version.

This Role has the following additional molecule test scenarios:
-   version-lock

Details can be found in ```molecule/```


## [Exceptions](#exceptions)

Some variations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| RedHat/CentOS/Fedora | Not fully tested because of weird behaviour while testing with molecule/Docker. |
| Rockylinux | Not fully tested because of weird behaviour while testing with molecule/Docker. |
| Almalinux | Not fully tested because of weird behaviour while testing with molecule/Docker. |
| Amazonlinux | Not officially supported. |
| Ubuntu 2204 | No release file ATM. |


If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-mongodb/issues)

## [License](#license)

MIT


## [Author Information](#author-information)

[Mullholland](https://github.com/mullholland)

## [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
