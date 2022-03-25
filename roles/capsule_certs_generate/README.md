redhat.satellite_operations.capsule_certs_generate
==================================================

Generates a certificate bundle for Satellite Capsule scenario

Role Variables
--------------

Required:

- `satellite_capsule_certs_generate_fqdn`: Target FQDN to generate a certificate bundle for

Optional:

- `satellite_capsule_certs_generate_tarball`: Full path of the tarball that should be generated. Defaults to /root/<satellite_capsule_certs_generate_fqdn>.tar.gz
- `satellite_capsule_certs_generate_options`: Array of options to pass to the installer

Example Playbooks
-----------------

Generate a certificate bundle for the hostname proxy.example.com:

```yaml
---
- hosts: all
  gather_facts: false
  vars:
    satellite_capsule_certs_generate_fqdn: proxy.example.com
  roles:
    - role: capsule_certs_generate
```
