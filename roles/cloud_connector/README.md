redhat.satellite_operations.cloud_connector
=====================================

Install and configure Red Hat Cloud Connector

Role Variables
--------------

Required:

- `satellite_cloud_connector_url`: The URL of the Satellite server.
- `satellite_cloud_connector_user`: The username cloud connector will use to talk to Satellite API.
- `satellite_cloud_connector_password`: The password cloud connector will use to talk to Satellite API.

Optional:

- `foreman_cloud_connector_http_proxy`: HTTP proxy for RHC to use

Example Playbooks
-----------------

Run the installer setting the initial admin password:
Configure Cloud Connector:

```yaml
- hosts: target-host
  roles:
    - role: redhat.satellite_operations.cloud_connector
      vars:
        satellite_cloud_connector_url: https://satellite.example.com
        satellite_cloud_connector_user: admin
        satellite_cloud_connector_password: changeme
```
