[![Build Status](https://travis-ci.org/wahidsadik/apache-virtual-host.svg?branch=master)](https://travis-ci.org/wahidsadik/apache-virtual-host)
[![Galaxy](https://img.shields.io/badge/galaxy-apache--virtual--host-green.svg)](https://galaxy.ansible.com/wahidsadik/apache-virtual-host)

Role Name
=========

An Ansible role to configure Apache virtual host.

The role does these:

- Creates and activates a virtual host with Apache.
- Doesn't configure HTTPS. You can use https://letsencrypt.org/ for that.

The role is available on Ansible Galaxy: [https://galaxy.ansible.com/wahidsadik/ansible-apache-role](https://galaxy.ansible.com/wahidsadik/apache-virtual-host).

To add this role from Ansible Galaxy, run: `ansible-galaxy install wahidsadik.apache-virtual-host`.

To add this from your Ansible `requirements.yml`, add this to the file:

    src: wahidsadik.apache-virtual-host


Requirements
------------

The `remote_user` needs to have `sudo` access or be `root` equivalent user.

Role Variables
--------------

The role defines the following variables in `defaults/main.yml`:

Variable name|Default value|Comment
-------------|-------------|-------
`add_www` | `false` | When `true`, www will be added as server alias.
`disable_default_site` | `false` | When `true`, default site code will be removed and virtual host will be deactivated.
`certbot_tls` | `false` | When `true`, `certbot-auto` will be used to create TLS certificate. Also see `certbot_tos_email` variable below.

Users must pass the following parameters (i.e. variables):

- `website`. It is assumed that the website assets will be available at `/var/www/{{website}}` location.
- `template`: Choice of `basic`, `laravel` and `relative`.
  - `basic` sets document-root to `/var/www/{{website}}`.
  - `laravel` sets document-root to `/var/www/{{website}}/public`.
  - `relative` sets document-root to `/var/www/{{website}}/{{relative_path}}`.
    - Requires additional definition of `relative_path`.
- `certbot_tos_email`: When `certbot_tls` is `true`, this should be provided. Email address.

Example values for `domain`:

- example.com
- abc

Known issues
------------

- #1 - When `certbot_tls` os `true`, the role generates only one TLS certificate even when `add_www` is `true`. As as result, `https://www.example.com` will get an invalid certificate error.

Dependencies
------------

Apache2 must be installed on the hosts.

Example Playbook
----------------

Example 1: Simplest example with minimum variable passing

    - hosts: servers
      remote_user: root
      roles:
      - {
          role: wahidsadik.ansible-role-apache,
          website: example.com,
          template: basic
        }

Example 2: With sudo and minimum variable passing

    - hosts: servers
      remote_user: deployer
      become: true
      become_method: sudo
      roles:
      - {
          role: wahidsadik.ansible-role-apache,
          website: example.com,
          template: laravel
        }

License
-------

MIT

Author Information
------------------

Wahid Sadik. More at: [https://wahidsadik.github.io](https://wahidsadik.github.io).
