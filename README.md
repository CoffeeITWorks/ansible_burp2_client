

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


Check also all vars in `defaults/main.yml` you can override any default using your host/group_vars
There are vars to choose burp version and more.


Dependencies
------------


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

