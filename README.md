Ansible role mariadb
=========

Ansible for installing mariadb database. Role also creates users (for created databases or for existing databases), databases and option files.

Requirements
------------

None

Role Variables
--------------

#### `mariadb_root_password` (required)
mariadb root user password


#### `mariadb_default_collation` (optional)
default database collation

#### `mariadb_default_encoding` (optional)
default database encoding

#### `mariadb_default_user_host` (optional)
default host for users

#### `mariadb_databases` (optional)
Creates database and configures a user with password for it. For example:

 ```
 - database: mydb
   username: mydb
   password: reallygoodpassgoeshere
 ```

#### `mariadb_additional_privileges` (optional)

Used for creating user accounts for existing databases. For example:

 ```
 - database: mydb
   username: backupuser
   password: anotherreallygoodpassgoeshere
   privileges: mydb.*:SELECT,LOCK TABLES,SHOW VIEW,TRIGGER
   host: myserver.fqdn
 ```

#### `mariadb_option_files` (optional)

Creates .my.cnf files for users. For example,

```
mariadb_option_files:
  - name: zabbix
    path: /etc/zabbix/.my.cnf
    owner: zabbix
    group: zabbix
    mode: "0600"
    serole: system_r
    setype: zabbix_agent_t
    content: |
      # Managed by ansible
      [mysql]
      user=zabbix
      password=XXXXXXXXXXXXXXXXXXXXXXXXXX
      [mysqladmin]
      user=zabbix
      password=XXXXXXXXXXXXXXXXXXXXXXXXXX
```

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role, ansible-role-mariadb, tags: mariadb }

License
-------
Propriertary

Author Information
------------------
Tuomas Vallaskangas
