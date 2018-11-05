### Introspect
- create introspect json file
- `openstack baremetal import --json <filename>`
- - verify the node is now available
- `openstack baremetal node manage <node name>`
- - makes it manageable
- `openstack overcloud node introspect --all-manageable --provide`
- `openstack baremetal node set --property "cpapbilities=profile:<profile name>,boot_option:local"`
- edit the environment file settings to increate the number of nodes
- `openstack overcloud deploy --templates <templates folder> --environment-directory <path to environment folder>`

 
### Shared Storage
Prepare the controller
 - sudo su -
 - `yum -y install nfs-utils`
 - `iptables -v -I INPUT -p tcp --dport 2049 -j ACCEPT`
 - `service iptables save`
 - verify the External Network IP of compute0 and compute1 by pinging them
     - append `/etc/exports` with `/var/lib/nova/instances <compute external IP>(rw,sync,fsid=0,no_root_squash)`
     - enable nfs `systemctl enable nfs --now`
     - confirm the directory is exported `exportfs`
     - update vnc_listen in /etc/nova/nova/conf
     - - `openstack-config --set /etc/nova/nova.conf DEFAULT vnc_listen 0.0.0.0`
     - restart the compute services
     - - `openstack-service restart nova`

Prepare the compute nodes:
 - sudo su -
 - update fstab to mount the instances directory
 - - `echo '<controller external IP>:/ /var/lib/nova/instances nfs4 context="system_u:object_r:nova_var_lib_t:s0" 0 0' >> /etc/fstab`
 - mount the instances folder
 - - `mount -v /var/lib/nova/instances`
 - configure iptables to allow ports 16509 and range 49152-49261
     - - `iptables -v -I INPUT -p tcp --dport 16509 -j ACCEPT`
     - - `iptables -v -I INPUT -p tcp --dport 49152:49261 - ACCEPT`
     - - `service iptables save`
 - update vnc_listen in qemu.conf
     - -  ```cat <<EOF >> /etc/libvirt/qemu.conf```
          ```user="root"```
          ```group="root"```
          ```vnc_listen="0.0.0.0"```

 - configure properties in nova.conf to use the nft mount
 - - `openstack-config --set /etc/nova/nova.conf libvirt images_type default`
 - - `openstack-config --set /etc/nova/nova.conf DEFAULT instances_path /var/lib/nova/instances`
 - - `openstack-config --set /etc/nova/nova.conf DEFAULT novncproxy_base_url http://<controller external IP>:6080/vnc_auto.html`
 - - `openstack-config --set /etc/nova/nova.conf DEFAULT vncserver_listen 0.0.0.0`
 - - `openstack-config --set /etc/nova/nova.conf DEFAULT live_migration_flag VIR_MIGRATE_UNDEFINE_SOURCE,VIR_MIGRATE_PEER2PEER,VIR_MIGRATE_LIVE`
 - restart the openstack services
 - - `openstack-service restart`
     



 --------------------------
