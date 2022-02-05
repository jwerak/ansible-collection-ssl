# Ansible Collection - jwerak.ssl

My homelab collection to generate and distribute ssl certs for my domains.

Roles:
- *ssl_setup*
  - Setup letsencrypt certbot on fedora server
- *ssl_domain*
  - Generate certificates on my fedora-iot box for given domain
  - Configure renewal systemd timer unit (empty file is created for each domain to be deployed)
- *ssl_turris*
  - distribute ssl certs for domain to turris
  - configure ssl for admin portals
  - configure auto-update of cert update after renewal
    - systemd timer unit copying certs and restarting service
- *ssl_common_vars*
  - place to define common variables
