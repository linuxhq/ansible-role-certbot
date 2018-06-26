# ansible-role-certbot

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-certbot.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-certbot)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-certbot-blue.svg?style=flat)](https://galaxy.ansible.com/linuxhq/certbot)
[![License](https://img.shields.io/badge/license-GPLv3-brightgreen.svg?style=flat)](COPYING)

RHEL/CentOS - Automatically enable HTTPS

## Requirements

This role requires that you have the epel repository installed.

 * https://galaxy.ansible.com/linuxhq/epel/

This role uses the DNS authentication method via CloudFlare.  Other methods are not supported.

## Role Variables

Available variables are listed below, along with default values:

    certbot_args:
      - '--no-self-upgrade'
    certbot_basedir: /etc/letsencrypt
    certbot_cloudflare_api_key: ''
    certbot_cloudflare_email: ''
    certbot_domains: []
    certbot_email: root@localhost
    certbot_hookdir: "{{ certbot_basedir }}/manual-hooks"
    certbot_manual_auth_hook: "{{ certbot_hookdir }}/authenticator.sh"
    certbot_manual_cleanup_hook: "{{ certbot_hookdir }}/cleanup.sh"
    certbot_pre_hook: ''
    certbot_post_hook: ''
    certbot_renew_hook: ''

## Dependencies

None

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.certbot
          certbot_cloudflare_api_key: 2f6928177c97bfb515a6271704d7c5c4
          certbot_cloudflare_email: cloudflare@linuxhq.org
          certbot_domains:
            - www.linuxhq.org
            - www.linuxhq.net
          certbot_email: certbot@linuxhq.org
          certbot_post_hook: 'systemctl restart httpd.service'

## License

Copyright (C) 2018 Taylor Kimball <tkimball@linuxhq.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program. If not, see <http://www.gnu.org/licenses/>.
