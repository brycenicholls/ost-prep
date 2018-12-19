### Create a Linux Bridge

- verify `bridge-utils` is installed
- - `rpm -q bridge-utils`
 
- create the bridge file
- - `vi /etc/sysconfig/network-scripts/ifcfg-br-name`
   ```
    DEVICE=br-name
    TYPE=bridge
    ONBOOT=yes
    BOOTPROTO=static
    IPADDR=x.x.x.x
    NETMASK=x.x.x.x
    ```
    
- link the brodge to an interface
    - `vi /etc/sysconfig/network-scripts/ifcfg-eth1`
    ``` 
        DEVICE=eth1
        TYPE=Ethernet
        ONBOOT=yes
        BRIDGE=br-name
    ```
- restart the network service
- - `systemctl restart network`
 
- verify
- - `brctl show`