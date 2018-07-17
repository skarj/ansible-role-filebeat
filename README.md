Filebeat role
=========
[![Build Status](https://api.travis-ci.org/skarj/ansible-role-filebeat.svg?branch=master)](https://travis-ci.org/skarj/ansible-role-filebeat)

Ansible role for [filebeat](https://www.elastic.co/products/beats/filebeat) 6.x installation.
Versions lower than 6 are not supported by this role.

Requirements
------------

* Ansible 2.5
* This role requires [hash_behaviour=merge](http://docs.ansible.com/ansible/latest/reference_appendices/config.html#default-hash-behaviour) for variables


Dependencies
------------

None


Role Variables
--------------

Default config variables are described in *defaults/main.yml*.
If you need an extended configuration you can specify it in the variables for each environment in section *filebeat.options*.
Structure of section *filebeat.options* repeats *filebeat.yml*, you can insert any parameters described in official filebeat [documentation](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-configuration-details.html)


Example Playbook
----------------

An example of how to use this role:

    - hosts: all
      roles:
        - role: ansible-role-filebeat
          filebeat:
            options:
              filebeat:
                prospectors:
                  - type: log
                    fields:
                      log_type: syslog
                      project: devops
                      environment: "dev"
                    document_type: syslog
                    paths:
                      - /var/log/cron
                      - /var/log/secure
                      - /var/log/messages
                      - /var/log/yum.log
              output:
                logstash:
                  hosts:
                    - logstash:5044
                  index: filebeat


License
-------

MIT


Author Information
------------------

Sergey Baranov <skaarj.sergey@gmail.com>
