# ansible-role-certbot

[![Build Status](https://travis-ci.org/linuxhq/ansible-role-certbot.svg?branch=master)](https://travis-ci.org/linuxhq/ansible-role-certbot)

RHEL/CentOS - Automatically enable HTTPS

## Requirements

This role uses the DNS authentication method via CloudFlare.  Other methods are not supported.

## Role Variables

Available variables are listed below, along with default values:

    certbot_basedir: /etc/letsencrypt
    certbot_hookdir: "{{ certbot_basedir }}/manual-hooks"
    certbot_manual_auth_hook: "{{ certbot_hookdir }}/authenticator.sh"
    certbot_manual_cleanup_hook: "{{ certbot_hookdir }}/cleanup.sh"

Additional configuration variables which are __**required**__:

    certbot_domains: []
    certbot_cloudflare_api_key: ''
    certbot_cloudflare_email: ''
    certbot_email: ''

Additional configruation variables not defined by default:

    certbot_args: []
    certbot_pre_hook: ''
    certbot_post_hook: ''
    certbot_renew_hook: ''

## Dependencies

 * https://galaxy.ansible.com/linuxhq/epel/

## Example Playbook

    - hosts: servers
      roles:
        - role: linuxhq.certbot
          certbot_args:
            - '--no-self-upgrade'
          certbot_cloudflare_api_key: 2f6928177c97bfb515a6271704d7c5c4
          certbot_cloudflare_email: cloudflare@linuxhq.org
          certbot_domains:
            - www.linuxhq.org
            - www.linuxhq.net
          certbot_email: certbot@linuxhq.org
          certbot_post_hook: 'systemctl restart httpd.service'

## License

GPLv3

## Author Information

This role was created by [Taylor Kimball](http://www.linuxhq.org).
