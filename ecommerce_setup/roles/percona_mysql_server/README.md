# Ansible role for Percona Mysql Server

## Tested On

  * EL 7

## Description

The certbot role will install Percona Mysql packages.

After installation, basic application configuration can be controlled with variables.

## Usage

  * Drops the default test DB and anonymous users.
  * Generates a random root password, unless `mysql_root_password` is given. 
     * Password stored to the remote host @ `/root/.my.cnf`.
  * If given, `mysql_app_db` defines the name of the application database to be created.
  * If given, `mysql_app_user` defines the username that will be used to access the app database.
  * `mysql_app_privileges` defines the privileges to be set on the app user.
  * Generates a random password for application user, unless defined with `mysql_app_password`.
    * Application credentials stored to `{{ ansible_user_dir }}/.my.cnf`
    * After running the mysql role, the variable mysql_app_password is populated with the app password.

```yaml
    - hosts: appserver
      vars:
        mysql_app_db: "integration-app"
        mysql_app_user: "integration-app"
        mysql_app_privileges: "{{ mysql_app_db }}.*:ALL"
        app_mysql_password: "{{ mysql_app_password }}"
      roles:
        - { role: percona_mysql_server, become: yes, tags: mysql }
        - { role: application }
```
