eNiXHosting.beats
=========

An Ansible role to deploy Elastic [Beats](https://www.elastic.co/products/beats) modules shipper.

**Only one shipper can be installed at a time using this role. If you want to install several shippers, run the role multiple times**

Requirements
------------

Supported targets:

- Debian 8 "Jessie"
- Debian 9 "Stretch"
- RedHat EL 7


Role Variables
--------------

- `beats__shippper` - Beats software shipper to install. Supported: filebeat, metricbeat, heartbeat
- `beats__modules` - List of modules templates configuration files to add
- `beats__modules_sourcedir` - Modules templates directory. Default: `templates/`
- `beats__extra_options` - options to add at the end of configuration file
- `beats__logstash_enabled` - Is Logstash output enabled. Default: `false`
- `beats__logstash_index` - The index root name to write evetns to. Default: `beats`
- `beats__logstash_hosts` - The list of downstream Logstash servers. Default: `["localhost:5044"]`
- `beats__elasticsearch_enabled` - Is ElasticSearch output enabled. Default: `false`
- `beats__elasticsearch_hosts` - The list of downstream ElasticSearch servers. Default: `["localhost:9200"]`
- `beats__elasticsearch_protocol` - ElasticSearch connection protocl. Default: "http"
- `beats__elasticsearch_user` - If auth enabled, provide username
- `beats__elasticsearch_password` - If auth enabled, provide password

Dependencies
------------

Ansible roles, can be pulled by ansible-galaxy or by hand in roles/

- `eNiXHosting.elastic_repo`: https://galaxy.ansible.com/eNiXHosting/elastic_repo/.


Usage
-----

Clone this repo into your roles directory:

    $ git clone https://gitlab.enix.org/ansible/ansible-beats.git roles/beats

Or use Ansible galaxy requirements.yml

    # eNiXHosting.beats galaxy role
    - src: eNiXHosting.beats

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: eNiXHosting.beats
           elastic_repo__branch: 6.x
           beats__shippper: "filebeat"
           beats__elasticsearch_enabled: true
           beats__elasticsearch_hosts: ["192.168.1.1:9200", "192.168.1.2:9200"]
           beats__modules: ['system.yml.j2']
           beats__modules_sourcedir: "modules/"
           beats__extra_options: |
             xpack.monitoring.enabled: true
             logging.level: debug

Or can be configured in inventory files this way using oneliner:
```
[all:vars]
beats__logstash_hosts=["toto:5004"]
beats__modules=["system.yml.j2"]
```

TODO
-----

List of stuff to improve in this role
- readd tls stuff when needed

License
-------

GPLv2

Author Information
------------------

Laurent CORBES, Based on Artur Melo work at https://github.com/Restless-ET/ansible-role-beats
