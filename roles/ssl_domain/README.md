Role Name
=========

Simple role to create ssl certs using LetsEncrypt, Google DNS and podman.

Requirements
------------

- Domain managed by Google Cloud DNS
- Authenticated as user with proper privileges
- ansible collections:
  - `ansible-galaxy collection install containers.podman`


Create GCloud privileged SA and local credentials:
- create [service account](https://developers.google.com/identity/protocols/oauth2/service-account#creatinganaccount)
- Grant [Letsencrypt privileges](https://certbot-dns-google.readthedocs.io/en/stable/#credentials) to [the service account](https://cloud.google.com/dns/docs/access-control#permissions_and_roles)
- json saved in *~/.secret/letsencrypt-dns-admin.json*


Execution Flow
--------------

All commands are to be executed in podman container.

Stage 1: Create certificate using certbot
- verify if prerequisities are installed
- Copy secret to server
- Podman steps
  - ensure image is downloaded /docker.io/certbot/dns-google:latest/
  - Create [podman secret](https://www.redhat.com/sysadmin/new-podman-secrets-command) with google credentials
- Generate certificate
  - ```
    certbot certonly \
      --dns-google \
      --dns-google-credentials /run/secrets/google.json \
      -d example.com
    ```

Stage 2: Create systemd units to update certs when obsolete

- Create renewal systemd-timer
  - `certbot renew`

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
