Role Name
=========

This role installs [Beats](https://www.elastic.co/products/beats) products (e.g. Filebat, Metricbeat, etc.)on a Ubuntu machine.

Requirements
------------

None

Role Variables
--------------

You should specify the version for the Beats products you want to install with the `beats_ver` variable (default: 6.2.2).

Also you need to specify the products you want to install in a list variable called `products`:
```
products:
  - filebeat
  - metricbeat
```

Dependencies
------------

There is no dependencies

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: jobscore.beats
           products:
            - filebeat
            - metricbeat
            - heartbeat

License
-------

GPLv3

Author Information
------------------

This role was created by [Eric Magalhães](https://emagalha.es)
