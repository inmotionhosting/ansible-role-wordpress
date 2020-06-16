inmotionhosting.wordpress
=========

Modular Ansible Role for deploying and configuring WordPress.

[![Build Status](https://travis-ci.org/inmotionhosting/ansible-role-wordpress.png?branch=master)](https://travis-ci.org/inmotionhosting/ansible-role-wordpress)

Requirements
------------

* CentOS 7.x or later
* Debian 9 or later
* Ubuntu 16.04 LTS or later

Role Variables
--------------

### Defaults
Variables in `defaults/main.yml`

| Variable | Definition |
| -------- | ---------- |
| pass_gen_alias | A variable acting as an alias to generate safe passwords.
| site_domain | The domain to associate with the WordPress installation.
| site_email | The email to associated with the WordPress administrative account.
| site_user | The username to associated with the WordPress administrative account.
| site_pass | The password to associated with the WordPress administrative account.
| system_user | The system user that the WordPress site will belong to.
| wp_db_name | The name of the database to associate with this WordPress installation.
| wp_db_user | The name of the database user account to associate with this WordPress installation.
| wp_db_pass | (Optional) The password to associate with the `wp_db_user`.  If not defined, the password will be automatically generated via `pass_gen_alias`.
| wp_plugins | The list of WordPress plugins to install.  Note that plugins are only installed in fresh deployments of WordPress; changing this list and redeploying will not add/remove plugins fron an existing installation of WordPress.
| wp_system_folder | The name of the folder WordPress should be installed to within the `system_user`'s home directory.
| wp_system_path | The full path to the `system_user`'s `wp_system_folder`.
| max_request_workers | Apache: The number of simultaneously connections allowed. Must be a multiple of 25.
| php_proc_mem: | PHP-FPM: Memory consumption per PHP worker.
| children_buffer | PHP-FPM: What percentage of the server's memory PHP can consume.

Dependencies
------------

### Required

```yaml
- role: inmotionhosting.apache
- role: inmotionhosting.mysql
- role: inmotionhosting.php_fpm
```

Example Playbook
----------------

```yaml
- hosts: wordpress_lamp
  roles:
    - role: inmotionhosting.apache
    - role: inmotionhosting.mysql
    - role: inmotionhosting.php_fpm
    - role: inmotionhosting.wordpress
```

License
-------

GPLv3

Author Information
------------------

[InMotion Hosting](https://inmotionhosting.com)
