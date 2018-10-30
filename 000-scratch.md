https://www.redhat.com/en/services/training/ex210-red-hat-certified-system-administrator-red-hat-openstack-exam

- readup on `policy.json`
    - eg: /etc/keystone/policy.json
 
- rpm -q <package name>


Storage:
- Swift Object Storage
    - /var/log/swift/swift.log
    - /var/log/messages _for HAProxy, Swift config and CLI tool requests_
    - /et/swift/object-server.conf 
        - object-replicator _for replication conf_
        - object-updater _for information management_
        - object-auditor _for integrity information_
    - Detecting failed drives
        - swift-drive-audit
            - output goes to /var/log/kern.log
        - 