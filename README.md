# Ansible role for MySQL

This is a simple role that will install MariaDB and handle users, databases and configuration.

The role should work on all Debian-based distributions.

## Installation

Add this to your `requirements.yml`:

```yml
- src: https://github.com/angristan/ansible-mysql
```

## Sample playbook

```yaml
---

- hosts: myhost
  roles:
    - name: mysql
      tags: mysql
  vars:
    mysql_databases:
      - name: blog
      - name: forum
    mysql_users:
      - name: blog
        password: "{{ vault_mysql_password_blog }}"
        priv: 'blog.*:ALL'
      - name: forum
        password: "{{ vault_mysql_password_forum }}"
        priv: 'forum.*:ALL'
    mysql_options:
      - {section: mysqld, option: bind-address, value: 0.0.0.0}
      - {section: mysqld, option: innodb_buffer_pool_size, value: 1G}
      - {section: mysqld, option: innodb_io_capacity, value: 4000}
```
