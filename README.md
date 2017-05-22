Ansible Role Openproject
===============================================

Ansible role to install and configure openproject on gentoo instances.

Supported Distributions
-----------------------

- Gentoo

Requirements
------------

This role has a variety of dependencies. Please take a look at the example playbook.

Role Variables
--------------

None.

Dependencies
------------

[vundb/ansible-role-apache](https://github.com/vundb/ansible-role-apache)

[vundb/ansible-role-mysql](https://github.com/vundb/ansible-role-mysql)

[vundb/ansible-role-mysql-admin](https://github.com/vundb/ansible-role-mysql-admin)

[vundb/ansible-role-apache-vhost](https://github.com/vundb/ansible-role-apache-vhost)

[vundb/ansible-role-portage](https://github.com/vundb/ansible-role-portage)

Example Playbook
----------------
```
- hosts: all
  roles:
    - role: vundb-apache
      apache_opts: ["PASSENGER"]
    - role: vundb-mysql
      mysql_config:
        - { section: "mysqld", option: "sql_mode", value: "'no_auto_value_on_zero,strict_trans_tables,strict_all_tables,no_zero_in_date,no_zero_date,error_for_division_by_zero,no_auto_create_user,no_engine_substitution'" }
    - role: vundb-mysql-admin
      mysql_databases:
        - name: openproject
      mysql_users:
        - name: openproject
          pass: openproject
          priv: openproject.*:ALL
    - role: openproject
    - role: apache-vhost
      apache_vhosts:
        - label: "openproject"
          virtual_host: "*:80"
          server_name: "openproject.local"
          server_alias: "openproject.local"
          document_root: "/home/openproject/application/public"
          template: "templates/vhost-openproject.j2"
```

License
-------

MIT

Author Information
------------------

- You can find more roles in my GitHub channel [vundb](https://github.com/vundb)
- Follow me on Twitter [@vundb](https://twitter.com/vundb)
