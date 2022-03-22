redhat.satellite_operations.satellite_repositories
==================================================

Configure repositories required for deploying Satellite

Role Variables
--------------

Required:

- `satellite_repositories_version`: The version of Satellite to enable repositories for

Optional:

- `satellite_repositories_type`: Enable repositories for `satellite` (default) or `capsule`

Example Playbooks
-----------------

Configure repositories for Satellite 6.10:

```yaml
- hosts: target-host
  roles:
    - role: redhat.satellite_operations.satellite_repositories
      vars:
        satellite_repositories_version: '6.10'
```
