Solr Configuration as Slave
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-solr-slave/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-solr-slave.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-solr-slave)
[![Build Status](https://gitlab.com/lean-delivery/ansible-role-solr-slave/badges/master/build.svg)](https://gitlab.com/lean-delivery/ansible-role-solr-slave)
[![Galaxy](https://img.shields.io/badge/galaxy-lean__delivery.solr-slave-blue.svg)](https://galaxy.ansible.com/lean_delivery/solr-slave)
![Ansible](https://img.shields.io/ansible/role/d/30434.svg)
![Ansible](https://img.shields.io/badge/dynamic/json.svg?label=min_ansible_version&url=https%3A%2F%2Fgalaxy.ansible.com%2Fapi%2Fv1%2Froles%2F30434%2F&query=$.min_ansible_version)
## Summary

This role:
  - Configures Solr on Centos 7, Ubuntu or Windows host to be slave.

Requirements
------------
  - Minimal Version of the ansible for installation: 2.7
  - **Java 8** [![Build Status](https://travis-ci.org/lean-delivery/ansible-role-java.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-java)
  - **Solr installed** [![Build Status](https://travis-ci.org/lean-delivery/ansible-role-solr-standalone.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-solr-standalone)
  - **Supported OS**:
    - CentOS
      - 7
    - Ubuntu
    - Windows
      - "Windows Server 2008"
      - "Windows Server 2008 R2"
      - "Windows Server 2012"
      - "Windows Server 2012 R2"
      - "Windows Server 2016"
      - "Windows 7"
      - "Windows 8.1"
      - "Windows 10"

[Prepared Windows System](https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html)

## Role Variables
  - `solr_version` - matches available version on https://archive.apache.org/dist/lucene/solr/. Tested versions 5.3-7.1.x

    default: `8.0.0`

  - `solr_dest_main_path` - root directory to store solr folder

    default: `/opt` for Linux

    default: `C:\Solr` for Windows

  - `solr_dest_path` - solr folder path

    default: `{{ dest_main_path }}/solr-{{ solr_version }}`

  - `solr_configset_path` - solr configset folder path

    default: `{{ solr_home }}/configsets` for Linux

    default: `{{ solr_dest_path }}\server\solr\configsets` for Windows

  - `solr_service_name` - solr service name

    default: `solr`

  - `solr_with_systemd` - to run solr as a service

    default: `True`

  - `configset_list` - list of configset directories

    default: `['default']`

  - `auto_populate_configset_list` - get all configset directories automatically

    default: `True`

  - `solr_master_defined_host` - solr master host name. If defined - it will be used, else first server from solr-master group from inventory file

    default: `undefined`

  - `master_group` - solr master group name in inventory file

    default: `solr-master`

  - `solr_port` - solr master port

    default: `8983`

  - `solr_base_path` - path to solr base

    default: `/var/solr`

  - `solr_home` - path to SOLR_HOME

    default: `{{ solr_base_path }}/data`

  - `solr_ssl_enabled` - defined if solr master using ssl for connection

    default: `True`


Example Inventory
----------------
```ini
[solr-master]
solr-master.example.com

[solr-slave]
solr.example.com

[solrwin-slave]
solrwin.example.com

[solrwin-slave:vars]
ansible_user=admin
ansible_password=password
ansible_connection=winrm
ansible_winrm_server_cert_validation=ignore
```

Example Playbook
----------------

```yml
- name: Configure Solr as slave
  hosts: solr-slave
  roles:
    - role: lean_delivery.java
    - role: lean_delivery.solr_standalone
    - role: lean_delivery.solr_slave
```

License
-------

Apache

Author Information
------------------

authors:
  - Lean Delivery Team <team@lean-delivery.com>
