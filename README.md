
[![Build Status](https://travis-ci.com/CoffeeITWorks/ansible_burp2_client.svg?branch=master)](https://travis-ci.com/CoffeeITWorks/ansible_burp2_client)

[![Molecule](https://github.com/CoffeeITWorks/ansible_burp2_client/actions/workflows/molecule-test.yml/badge.svg)](https://github.com/CoffeeITWorks/ansible_burp2_client/actions/workflows/molecule-test.yml)

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

Add to your host/group_vars
---------------------------

Create host_vars or group_vars dirs.

Inside it you can add a file with the name of the group or the host where you want to add specific options of this role.

*Required vars*:

```yaml
# You should change these in your group_vars/host_vars
burp_client_server: "192.168.0.1"      # IP of burp server
burp_client_ssl_peer_cn: "burpserver"  # Hostname of burp server
burp_client_password: "password" # same password as set in incexc on server side
```

When you use group per location and have a burp2 server per location, you can use these variables per location/group.

*Options vars:*

```yaml
burp_server_port_per_operation_bool: true
burp_client_port: "{{ burp_server_port | default(4971) }}"
burp_client_status_port: "{{ burp_server_status_port | default(4972) }}"

burp_client_pidfile: "/var/run/burp.pid"
```

Port per operation
------------------

---

Since version 2.1.10

* Add the ability for the client to connect to different server ports

 according to whether it is doing backup/restore/verify/list/delete.
 These ports are based on: https://github.com/CoffeeITWorks/ansible_burp2_server/issues/11
 Compatible since burp 2.1.10

```yaml
burp_server_port_per_operation_bool: True

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

License
-------

MIT

Author Information
------------------

This role was main developed by Diego Daguerre with collaboration of Pablo Estigarribia (pablodav at gmail)

Collaborators
-------------

* @planet-winter (Daniel Winter): FreeBSD 11 support

Burp backup and restore
=======================

Main page: http://burp.grke.org/

Burpui
======

Main page: https://git.ziirish.me/ziirish/burp-ui

Testing with molecule v2 (for devs)
===================================

For defaults linux tests,
You can check the steps in [.travis.yml](.travis.yml)

And use standard tests too:

    sudo molecule test

For FreeBSD 11 you can also use [molecule/freebsd/INSTALL.rst].
Then use scenario *freebsd*:

```shell
molecule create -s freebsd
molecule converge -s freebsd
molecule idempotence -s freebsd
molecule destroy -s freebsd
```
