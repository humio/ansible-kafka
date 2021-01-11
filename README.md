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
kafka_broker_rack: dc1
zookeeper_hosts:
- ip: "{{ ansible_default_ipv4.address }}"
```

On machines without internet access `kafka_mirror` can be set to `"master"` to copy the Kafka tarball from the master's files directory

```yaml
kafka_mirror: "master"
```

Rack Awareness
------------

Kafka supports rack awareness if you specify which rack each Kafka node is in. This can be done by
setting the `broker.rack` setting in Kafka. This is configured in this Ansible role via the
`kafka_broker_rack` variable. To have this work properly, make sure each rack or datacenter is
defined as a group in your inventory and the appropriate machines are assigned. You can then either
set the `kafka_broker_rack` variable directly inside the inventory or you can create a `group_vars`
file for each of the rack/datacenter groups that defines it appropriately.

By default, all Kafkas are assigned to a single rack named `dc1`.

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

Troubleshooting
---------------

If you're forced to interrupt the ansible run during the `Install Kafka from remote` step, you may run into a situation
where the tarball that's being fetched and unarchived was interrupted during the unarchive phase. If this step is
interrupted while the tarball is still being fetched (e.g., a timeout), then you're fine to simply re-run the playbook
again. If it happens during the unarchive phase, you will need to manually clear the
`/usr/lib/kafka_{{ kafka_scala_version }}-{{ kafka_version }}` directory before running the playbook again (this stage
checks for the existance of that directory to skip the step in future runs). 

License
-------

Apache
