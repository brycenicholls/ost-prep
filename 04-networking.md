### NOTE

enabling NetworkManager is a bad idea on  OpenStack because it tries to automatically configure the network interfaces.
This can be mitigated by

- - NM_CONTROLLED=no
- - systemctl disable NetworkManager

- location of interface config
    - `/etc/sysconfig/network-scripts/ifcfg-eth0`




- lspci 
- ethtool -i `<interface>`  _to view the network driver_
- ip link show `<interface>`
- ip link set up x`<interface>`
- ip link set down `<interface>`
- nohup tcpdump -nvv -i `<interface>` > name.txt 2>/dev/null &
- 
- 

## Tasks
- add an ephemeral address to an interface
    - ip a a 10.1.1.1/24 brd + dev eth1
- verify the address has been assigned
    - ip a s dev eth1
- run tcpdump to run captures on an interface
    - nohup tcpdump -n -i eth1 > name.pcap 2>/dev/null &  (this runs a background process)
        - `jobs` (lists the process)
        - `kill %<job number>` (to stop the process)

-  send ICMP over a specified interface
    - ping -I eth1 10.1.1.1

- edit eth1 to assign a static IP (centOS)
    - vi /etc/sysconfig/network-scripts/ifcfg-eth1
    ```
        DEVICE=eth1
        TYPE=Ethernet
        BOOTPROTO=static
        IPADDR=10.1.1.1
        PREFIX=24
    ```
- restart the network service
    - `systemctl restart network.service`
---

## Linux Brigde

### `brctl` ###
ephemeral commands

    - `brctl addbr <bridge name>` (to add a bridge)
    - `brctl delbr <bridge name>` (to delete the bridge)
    - brctl addif 
    - brctl delif
    - brctl show
    - brctl showmacs

 
Static configuration

- Create a `ifcfg-bridgename` file in `/etc/sysconfig/network-scripts`

- in the interface config, associate the interface to the bridgename and set the type to Bridge.
    

## OVS Bridges

### Network Flow:

VM1 --> OVS Bridge -> GRE-Tunnel --> Physical host -> Physical Switch -> Physical host -> GRE-Tunnel -> OVS Bridge -> VM2 

### Commands:

- ovs-vsctl show
- ovs-vsctl add-br `<bridgename>`
- ovs-vsctl del-br
- ovs-vsctl list-br
- ovs-vsctl add-port `<bridgename>`
- ovs-vsctl del-port `<bridgename>`
- ovs-vsctl list-interfaces `<bridgename>`
- ovs-vsctl list-ports `<bridgename>`
- ovs-vsctl iface-to-br `<interface name>`

## OpenFlow

- ovs-ofctl show
- ovs-ofctl dump-ports-desc
- ovs-ofctl dump-flows

---

verify is openvswitch is installed

- rpm -q openvswitch
- systemctl status openvswitch
- systemctl start openvswitch
- systemctl enable openvswitch

