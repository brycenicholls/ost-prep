### Undercloud / Director commands

- `openstack compute service list`
    - ensure  nova is up and running
    - 
    - 

### Verify Overcloud 

openstack catalog list
openstack endpoint list

_pull list of tenants attached to a user using curl_

curl -H "X-Auth-Token:<token_id>" <keystone_catalog_public_url>/tenants | jq .


### Truncate Keystone Database

#### On the undercloud
```
mysql -u root
use keystone
SELECT table_name, (data_length+index_length) tablesize FROM information_schema.tables;
SELECT COUNT(*) FROM token WHERE token.expires < CONVERT_TZ(NOW(), @@session.time_zone, '+00.00');
TRUNKATE TABLE token;
SELECT COUNT(*) FROM token WHERE token.expires < CONVERT_TZ(NOW(), @@session.ime_zone, '+00.00');
exit
```
_check cron job exists_
```
crontab -u keystone -l
```

_modify crontab to run keystone flush hourly_
```
crontab -u keystone -e
```
