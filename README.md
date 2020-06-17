inmotionhosting.wordpress
=========

Modular Ansible Role for deploying and configuring WordPress.

[![Build Status](https://travis-ci.org/inmotionhosting/ansible-role-wordpress.png?branch=master)](https://travis-ci.org/inmotionhosting/ansible-role-wordpress)

# Requirements

* CentOS 7.x or later
* Debian 9 or later
* Ubuntu 16.04 LTS or later

# Role Variables

Available variables are listed below with their default values (you can also see `defaults/main.yml`)

### WordPress site installation options

```
site_domain: "{{ ansible_fqdn }}"
site_email: "email@example.com"
site_user: "example_username"
site_pass: "example_password"
```

Settings for installing a WordPress site. It's highly encouraged to change the email, user and pass for security reasons. If you change the site domain, make sure to set it to something that is pointed to the server. By default it will use the hostname that Ansible pulls from the server.

```
wp_plugins:
  - block-bad-queries
  - boldgrid-backup
  - health-check
  - heartbeat-control
  - w3-total-cache
```

WordPress plugins to install and activate.

___Note:___ If using the UltraStack optimizations it's highly recommended to use the `w3-total-cache` plugin.

### System user/path options

```
system_user: "wordpress"
```
This is the system user that the WordPress site will be installed to (this will be created if it doesn't exist).

```
wp_system_folder: "doc_root"
```

The folder that the WordPress installation will be installed to. This will be a folder within the system user's home folder.

```
max_request_workers: # Apache: The number of simultaneous connections allowed. Must be a multiple of 25.
php_proc_mem: # PHP-FPM: Memory consumption per PHP worker.
children_buffer # PHP-FPM: What percentage of the server's memory PHP can consume.
```

These are configuration settings for Apache and PHP.

### Database options

```
wp_db_name: "{{ system_user }}"
wp_db_user: "{{ system_user }}"
# wp_db_pass: 'not_secure'
```

These are database user/name for the WordPress installation.

___Note:___ By default the `wp_db_pass` is automatically generated for you, though this may be set to your desired password instead should this be preferred.

### Let's Encrypt

```
use_letsencrypt: false
```

Whether a Let's Encrypt SSL should be generated.

___Note:___ This should only be used when you have a domain pointed to the target WordPress installation.


# Dependencies

### Required

```yaml
- role: inmotionhosting.apache
- role: inmotionhosting.mysql
- role: inmotionhosting.php_fpm
```

# Example Playbook

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
