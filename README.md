humio.kafka
=========

Kafka installer for running together with Humio

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

On machines without internet access `kafka_mirror` can be set to `"master"` to copy the Kafka tarball from the master's files directory

```yaml
kafka_mirror: "master"
```

Dependencies
------------

Java 9 must be installed. [humio.java](https://galaxy.ansible.com/humio/java/) role is recommended

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
    - role: humio.java
    - role: AnsibleShipyard.ansible-zookeeper
    - role: humio.kafka
```

License
-------

Apache
