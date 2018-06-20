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
kafka_listeners:
- scheme: "PLAINTEXT"
  host: "{{ ansible_default_ipv4.address }}"
  port: 9092
kafka_broker_id: 0
zookeeper_hosts:
- ip: "{{ ansible_default_ipv4.address }}"
```

Dependencies
------------

Java 9 must be installed. [humio.ansible-java](https://github.com/humio/ansible-java) module is recommended

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: servers
  become: true
  vars:
	zookeeper_hosts:
	  - zookeeper_id: 1
	    ip: "{{ ansible_default_ipv4.address }}"
  roles:
    - role: humio.ansible-java
    - role: AnsibleShipyard.ansible-zookeeper
    - role: humio.ansible-kafka
```

License
-------

Apache
