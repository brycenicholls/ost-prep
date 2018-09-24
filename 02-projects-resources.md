## Topics ##
- Projects
  - Defaults:     
    - Admin
    - Services

2- User accounts

3- Roles and privileges
    Defaults: 
        `_admin_`
        `_member_`
4- Managing quotas







- create a user
    - openstack user create --project `<name>` --password `<password> <username>`
- delete a user
    - openstack user delete `<username>`
- disable a user
    - openstack user set --diable `<username>`


### Roles and Privileges

- create a role
    
- list roles
    - `openstack role assignment list --project <project_name> --user <username> --names`
- assign a role to a user
    - `openstack role add --project <project name> --user <username> <role: eg: _member_>` 
  
### Quotas

- View default quotas
    - `openstack quota show --default`
- Edit default quota
    - `nova quota-class-update default --instances 10`
- View project quotas
    - `openstack quota show <project name>`
- Edit project quotas
    - `openstack quota set --<properties> <project name>`
        - eg: `openstack quota set --ports 10 --subnets 5 my_project_name`