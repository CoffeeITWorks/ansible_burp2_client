
[![CircleCI](https://circleci.com/gh/CoffeeITWorks/ansible_burp2_client.svg?style=svg)](https://circleci.com/gh/CoffeeITWorks/ansible_burp2_client)

[![Build Status](https://travis-ci.org/CoffeeITWorks/ansible_burp2_client.svg?branch=master)](https://travis-ci.org/CoffeeITWorks/ansible_burp2_client)

Getting Started
================

Check the documentation added in: 

https://github.com/CoffeeITWorks/ansible-generic-help#getting-started


Role Name
=========

ansible burp2_client deploy and maintenance role.

This roles builds burp version specified on defaults/main.yml. 
Also configures it to get it working and maintained in a centralized way.


Requirements
------------

Have burp2_server configured, recommended use ansible_burp2_server role from CoffeeITWorks: https://github.com/CoffeeITWorks


Role Variables
--------------

### Add to your host/group_vars:
 
Create host_vars or group_vars dirs. 

Inside it you can add a file with the name of the group or the host where you want to add specific options of this role.

*Required vars*:

    burp_client_server: IP.ADD.RE.SS

*Options vars:* 

    burp_client_port: "{{ burp_server_port | default(4971) }}"
    burp_client_status_port: "{{ burp_server_status_port | default(4972) }}"
    burp_client_port_restore: "{{ burp_restore_port | default(4973) }}"
    burp_client_status_port_restore: "{{ burp_restore_status_port | default(4974) }}"

    burp_client_pidfile: "/var/run/burp.pid"
    burp_client_password: "password"
    burp_client_protocol: "1"


#### Port per operation

--- 

Since version 2.1.10
   + Add the ability for the client to connect to different server ports

 according to whether it is doing backup/restore/verify/list/delete.
 These ports are based on: https://github.com/CoffeeITWorks/ansible_burp2_server/issues/11
 Compatible since burp 2.1.10

```yaml
burp_server_port_per_operation_bool: true
# This option will disable the creation of /etc/burp/burp-restore.conf too

# Default optional vars to change:
# These are not needed to be changed, but showing here the
# defaults that we have in defaults/main.yml
burp_server_port_operation_restore: 4975
burp_server_port_operation_verify: 4976
burp_server_port_operation_list: 4977
burp_server_port_operation_delete: 4978
```

Check also all vars in `defaults/main.yml` you can override any default using your host/group_vars
There are vars to choose burp version and more.

These options **will setup** `/etc/burp/burp.conf`

Dependencies
------------

Upgrading your OS
-----------------

Please note when using compiled version of burp with this role, after you upgrade your linux distribution is very recommended to run recompile and install of burp. 

Example to run it once:

    ansible-playbook -i production burp-client.yml -l client -e "burp_force_reinstall=yes"

The variable `burp_force_reinstall: yes` will do it for you.


License
-------

MIT

Author Information
------------------

This role was main developed by Diego Daguerre with collaboration of Pablo Estigarribia (pablodav at gmail)

Burp backup and restore
=======================

Main page: http://burp.grke.org/

Burpui
======

Main page: https://git.ziirish.me/ziirish/burp-ui

