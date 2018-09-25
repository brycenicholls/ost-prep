### Verifying services


## install openstack-utils
yum -y install openstack-utils

- check status of all services
    - `openstack-status`
- check individual service status
    - `openstack-service status <service name>`

-  restart a service
    - `openstack-service restart <service name>`