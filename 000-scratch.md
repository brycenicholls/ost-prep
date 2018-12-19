Expanding overcloud
creating a message queue and adding a message
creating an external network looking at the ml2 config
creating a stack: More prep needed
working out the stackrc password
lookup error 500 no suitable host found error when creating a stack and also when creating an instance
workout the minimum flavor for a rhel instance
===============================================

Before the exam:

- UNDERCLOUD
- - check services
-- 

- OVERCLOUD
- - verify correct rcfile
- - verify services
- - log onto each node using heat-admin and verify services and interfaces.
    - CONTROLLER:
        - `ip a s` Verify eth, vlan and br-ex
        - `sudo ovs-vsctl list-br `
        - `sudo ovs-vsctl list-ifaces br-trunk`
        - `sudo ovs-vsctl list-ifaces br-ex`
        - `systemctl -t service list-units open\* neutron\* ceph\*` to verify services are loaded
    
    - COMPUTE:
        - `ip a s`
        - `sudo ovs-vsctl list-br`
        - `sudo ovs-vsctl list-ifaces br-trunk`
        - `systemctl -t service list-units open\* neutron\* ceph\*`

    - CEPH:
        - `ip a s`
        - `sudo ovs-vsctl show`
        - `systemctl -t service list-units ceph\* open\* neutron\*`
        - `sudo ceph ceph status`
        - `sudo ceph osd lspools`
        - `sudo ceph osd ls`
        - `sudo ceph osd tree`
        - `lsblk -fs`




# MESSAGE BROKER
lab communication-msg-brokering setup

- From workstation, use SSH to connect to director as the stack user. Use sudo to become the root user.
- Create a rabbitmq user named rabbitmqauth with redhat as the password.  
- Configure permissions for the rabbitmqauth user. Use wildcard syntax to assign all resources to each of the three permissions for configure, write, and read.
- Set the administrator user tag to enable privileges for rabbitmqauth.
- Verify that a RabbitMQ Management configuration file exists in root's home directory. The contents should match as shown here.

- Verify that rabbitmqauth is configured as an administrator.
- Create an exchange topic named name.topic.
- Verify that the exchange topic is created.
- The next practice is to observe a message queue. Create a queue named redhat.queue
- Publish messages to the redhat.queue queue. These first two examples include the message payload on the command line.

- Verify the queue message count

- Display the first message in the queue. The message_count field indicates how many more messages exist after this one.
- Display multiple messages using the count option. Each displayed message indicates how many more messages follow. The redelivered field indicates whether you have previously viewed this specific message.
- When finished, delete the queue named redhat.queue. Return to workstation
