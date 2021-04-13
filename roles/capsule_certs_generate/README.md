redhat.satellite-operations.satellite_proxy_certs_generate
==================================================

Generates a certificate bundle for Katello scenario

Role Variables
--------------

Required:

- `satellite_proxy_certs_generate_fqdn`: Target FQDN to generate a certificate bundle for

Optional:

- `satellite_proxy_certs_generate_tarball`: Full path of the tarball that should be generated. Defaults to /root/<satellite_proxy_certs_generate_fqdn>.tar.gz
- `satellite_proxy_certs_generate_options`: Array of options to pass to the installer

Example Playbooks
-----------------

Generate a certificate bundle for the hostname proxy.example.com:

```
---
- hosts: all
  gather_facts: false
  vars:
    satellite_proxy_certs_generate_fqdn: proxy.example.com
  roles:
    - role: satellite_proxy_certs_generate
```
