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