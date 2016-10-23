[![Build Status](https://travis-ci.org/wahidsadik/apache-virtual-host.svg?branch=master)](https://travis-ci.org/wahidsadik/apache-virtual-host)
[![Galaxy](https://img.shields.io/badge/galaxy-ansible--role--apache-green.svg)](https://galaxy.ansible.com/wahidsadik/apache-virtual-host)

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

No default variable defined.

Users must pass the following parameters (i.e. variables):

- `website`. It is assumed that the website assets will be available at `/var/www/{{website}}` location.
- `template`: Choice of `basic` and `laravel`.
  - `basic` sets document-root to `/var/www/{{website}}`.
  - `laravel` sets document-root to `/var/www/{{website}}/public`.

Example values for `domain`:

- example.com
- abc

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
