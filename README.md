# Ansible Collection - jwerak.ssl

My homelab collection to generate and distribute ssl certs for my domains.

Roles:
- ssl_create
  - Generate certificates on my fedora-iot box for given domain
  - Configure renewal systemd timer unit
- ssl_manage_turris
  - distribute ssl domain to turris
  - configure ssl for admin portals
  - configure auto-update of cert update after renewal
    - systemd unit starting after renewal successfully completes
