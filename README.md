![Ansible Molecule Pipeline](https://github.com/inmotionhosting/ansible-role-wordpress/actions/workflows/main.yml/badge.svg) [![GPL-3.0 License](https://img.shields.io/github/license/inmotionhosting/ansible-role-wordpress.svg?color=blue)](https://github.com/inmotionhosting/ansible-role-wordpress/blob/master/LICENSE) [![GitHub stars](https://img.shields.io/github/stars/inmotionhosting/ansible-role-wordpress.svg)](https://github.com/inmotionhosting/ansible-role-wordpress/stargazers)

![InMotion Hosting Ultrastack](https://www.inmotionhosting.com/wp-content/uploads/2024/01/ultrastack-logo-black-vertical.png)

# Ansible Role: WordPress
Modular Ansible Role for deploying and configuring WordPress.

## Requirements
This Ansible role supports the two latest stable releases of specific
server-focused Linux distributions and aims to follow their deprecation
policies. Additionally we will focus on supporting the latest two stable
releases of each, which at the time of writing are as follows:

* CentOS 7.x
* Debian 11
* Ubuntu 20.04 LTS or later
* AlmaLinux 8.x or later
* RockyLinux 8.x or later

# Dependencies
```yaml
- collection: community.general
- collection: community.mysql
- collection: ansible.posix
```

# Role Variables
Available variables are listed below with their default values (you can also see `defaults/main.yml`)

### WordPress site installation options
```yaml
site_domain: "{{ ansible_fqdn }}"
site_email: "email@example.com"
site_user: "example_username"
site_pass: "example_password"
install_wordpress: true
```

Settings for installing a WordPress site. It's highly encouraged to change the email, user and pass for security reasons. If you change the site domain, make sure to set it to something that is pointed to the server. By default it will use the hostname that Ansible pulls from the server.

```yaml
wp_plugins:
  - block-bad-queries
  - boldgrid-backup
  - health-check
  - heartbeat-control
  - nginx-helper
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

```yaml
max_request_workers: # Apache: The number of simultaneous connections allowed. Must be a multiple of 25.
php_proc_mem: # PHP-FPM: Memory consumption per PHP worker.
children_buffer: # PHP-FPM: What percentage of the server's memory PHP can consume.
```

These are configuration settings for Apache and PHP.

### Database options
```yaml
wp_db_name: "{{ system_user }}"
wp_db_user: "{{ system_user }}"
# wp_db_pass: 'not_secure'
```

These are database user/name for the WordPress installation.

___Note:___ By default the `wp_db_pass` is automatically generated for you, though this may be set to your desired password instead should this be preferred.

### Let's Encrypt
```yaml
use_letsencrypt: false
```

Whether a Let's Encrypt SSL should be generated.

___Note:___ This should only be used when you have a domain pointed to the target WordPress installation.

## Example Playbook
```yaml
- hosts: wordpress
  roles:
    - role: inmotionhosting.wordpress
```

## License
GPLv3

## Author Information
[InMotion Hosting](https://inmotionhosting.com)
