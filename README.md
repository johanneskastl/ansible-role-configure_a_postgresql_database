![Ansible Lint](https://github.com/johanneskastl/ansible-role-configure_a_postgresql_database/workflows/Ansible%20Lint/badge.svg)

# configure_a_postgresql_database

Basic postgreSQL database configuration (users, permissions, etc.).

## Requirements

You need a PostgreSQL database installed and started.

## Role Variables

### Required variables

This role is intended to create a new user and database and set the appropriate
permissions for the user to use this database. Therefore you need to set some
variables for this role to work:

- `postgresql_login_password` (String): password for the administrative user
- `postgresql_database_name` (String): name of the database to be created
- `postgresql_user_name` (String):  name of the user to be created
- `postgresql_user_password` (String): password for the new user

### Privileged user

Normally the privileged user is called `postgres`. If this is not the case, you
can handover the user name using the following variable:

- `postgresql_login_user` (String): name of the administrative/privileged user

## User defaults

For the user login, the following defaults are used:

- `postgresql_user_contype` (String): contype, default is `host`
- `postgresql_user_login_method` (String): method, default is `md5`

## Database defaults

By default, the new database will be set up with the following default values:

- `postgresql_database_encoding` (String): encoding, default is `UTF-8`
- `postgresql_database_lc_collate` (String): lc_collate, , default is
  `en_US.UTF-8`
- `postgresql_database_lc_ctype` (String): lc_ctype, default is `en_US.UTF-8`
- `postgresql_database_template` (String): template to use, default is
  `template0`

### OS-related variables

Depending on your operating system, you might need to tweak the following
variables:

- `postgresql_service_name` (String): name of the PostgreSQL systemd service
  unit. Defaults to `postgresql.service`
- `postgresql_system_user` (String): name of the system user for PostgreSQL,
  defaults to `postgres`
- `psycopg2_package_name` (String): name of the package containing the Python
  module psycopg2, that is required by Ansible. Default is `python3-psycopg2`.

## Dependencies

None

## Example Playbook

```yaml
- hosts: servers
  roles:
    - role: 'johanneskastl.configure_a_postgresql_database'
      # Passwords should be in Ansible Vault, not in plaintext in a playbook...
      postgresql_login_user: 'postgres'
      postgresql_login_password: 'totallysecurepassword'
      postgresql_database_name: 'example-database'
      postgresql_user_name: 'example-user'
      postgresql_user_password: 'anothertotallysecurepassword'
```

## License

BSD-3-Clause
