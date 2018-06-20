Role Name
=========

A brief description of the role goes here.

Requirements
------------

This role must have access to an installation of Zookeeper

Role Variables
--------------

```yaml
kafka_mirror: http://mirrors.ae-online.de/apache/kafka
kafka_host: localhost
kafka_port: 9092
kafka_broker_id: 0
```

Dependencies
------------

Java 9 must be installed. [humio.ansible-java](https://github.com/humio/ansible-java) module is recommended

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: zookeepers
  become: true
  vars:
    zookeeper_url: http://dk.mirrors.quenda.co/apache/zookeeper/zookeeper-3.4.12/zookeeper-3.4.12.tar.gz
	zookeeper_hosts:
	  - zookeeper_id: 1
	    ip: 127.0.0.1
  roles:
    - role: humio.ansible-java
    - role: AnsibleShipyard.ansible-zookeeper
    - role: humio.ansible-kafka
```

License
-------

Apache
