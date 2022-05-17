# Ansible role for CertBot, the popular LetsEncrypt client

## Tested On

  * EL 7

## Description

The certbot role will provide and maintain a trusted SSL certificate for publicly-accessible instance upon which it is installed.

## Usage

  * Port 443 must be exposed and accessible from the public internet
  * The cert is created in standalone mode, meaning the Certbot process will bind to port 443 and listen for letsencrypt challenges. For this reason, this role should be run before the webserver.
  * The cert is renewed in webroot mode, expecting the webserver to serve the local dir defined by `certbot_auto_renew_webroot`

```yaml
    - hosts: webserver
      roles:
        - { role: certbot, become: yes }
        # certbot role should be run before application the depends on it
        - { role: nginx }
```
