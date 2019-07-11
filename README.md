Role Name
=========

This role installs [Beats](https://www.elastic.co/products/beats) products on a Ubuntu machine.

This role is capable of installing beats products available as deb packages. However, for configuring beats products (e.g filebeat.yml, metricbeat.yml) the only supported products so far are:

- filebeat
- metricbeat

Requirements
------------

None

Role Variables
--------------

You should specify the version for the Beats products you want to install with the `beats_version` variable (default: 6.7.2).

``` yaml
beats_version: 6.7.2
```


You also need to specify the products you want to install in a list variable called `beats_products` (default: []):

``` yaml
beats_products:
  - filebeat
  - metricbeat
```

If you want to hold beats packages on APT so they don't get updated (default: true) you can use the `beats_hold_products` variable:

``` yaml
beats_hold_products: true
```

If you want to also configure the products on the fly you will need to create a variable with the product name plus `_config:` which should be a dictionary containing the YAML config for the product you choose. E.G:

``` yaml
filebeat_config:
  filebeat.modules:
    - module: system
      syslog:
        enabled: true
  output.logstash.hosts:
    - logstash.server:5044

metricbeat_config:
  metricbeat.modules:
    - module: system
      metricsets: ["cpu","memory","network"]
      enabled: true
      period: 15s
      processes: ['.*']
  output.logstash.hosts:
    - logstash.server:5044
```
The specific values for the configuration are well described in the beats documentation


Dependencies
------------

There is no dependencies

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
``` yaml
- hosts: servers
  become: true
  roles:
    - role: jobscore.beats
      beats_version: 6.7.2
      beats_products:
        - filebeat
        - metricbeat
      filebeat_config:
        filebeat.modules:
          - module: system
            syslog:
              enabled: true
        output.logstash.hosts:
          - logstash.server:5044
      metricbeat_config:
        metricbeat.modules:
          - module: system
            metricsets: ["cpu","memory","network"]
            enabled: true
            period: 15s
            processes: ['.*']
        output.logstash.hosts:
          - logstash.server:5044
```
License
-------

GPLv3

Author Information
------------------

This role was created by [Eric Magalhães](https://emagalha.es)
