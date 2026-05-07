# Red Hat Satellite - Import Content Library

Ansible modules for interacting with the Satellite API importing content library.

## Requirements
Ansible 2.15 or higher

Red Hat Enterprise Linux 8 or higher

Valid Red Hat Subscriptions

## Variables

### Satellite Settings
|Variable Name|Default Value|Required|Type|Description|Example|
|:---|:---|:---:|:---:|:---|:---|
|`satellite_server_url`|"satellite.fqdn"|yes|string|Satellite server FQDN|satellite.domain.com|
|`satellite_username`|"admin"|yes|string|Username to access Satellite server|admin|
|`satellite_password`|"changeme"|yes|string|Password for Username that will be used to access Satellite server|changeme|
|`satellite_organization`|"Default Organization"|yes|string|Organization that this role be applied against|Default Org|

### Optional Settings
|Variable Name|Default Value|Required|Type|Description|Example|
|:---|:---|:---:|:---:|:---|:---|
|`satellite_validate_certs`|`false`|no|boolean|This setting validates certificate when using redhat.satellite modules||
|`satellite_operation_timeout`|7200|no|integer|Timeout in seconds|2 hours in seconds, integer|
|`satellite_poll_interval`|30|no|integer|Polling in seconds|30 seconds, integer|
|`satellite_max_retries`|3|no|integer|Polling in seconds|3 attempts, integer|
|`satellite_retry_delay`|30|no|integer|Polling in seconds|30 seconds, integer|
|`satellite_import_wait_time`|21600|no|integer|Polling in seconds|21600 seconds == 6 hours|

### Content View Settings
|Variable Name|Default Value|Required|Type|Description|Example|
|:---|:---|:---:|:---:|:---|:---|
|`satellite_timestamp`|"`{{ ansible_date_time['date'] }}`"|yes|string|||
|`satellite_directories`|"/var/lib/pulp"|yes|string|Satellite pulp directory||
|`satellite_import_content_library`|`true`|yes|boolean|Importing Content View Version||
|`satellite_import_lock_file`|"/tmp/satellite-import.lock"|yes|string|Importing Content View Version||
|`satellite_import_path`|"`{{ satellite_directories }}/imports`"|yes|string|Satellite Imports directory|/var/lib/pulp/imports|
|`satellite_import_content_library_metadata_file`|"`{{ satellite_import_path }}/metadata.json`"|yes|string|Metadata file for import|/var/lib/pulp/imports/metedata.json|
|`satellite_import_history`|`true`|yes|boolean|Importing Content View Version||
|`satellite_required_space_gb`|500|yes|integer|Default space required|500 is equal to 500GB|
|`satellite_cleanup_old_imports`|`false`|no|boolean|Optional clean up of old||
|`satellite_cleanup_old_import_age`|"30d"|yes|string|Age of imports to keep|7 days, 7d|
|`satellite_import_content_library_name`|""|yes|string|Content library name|Library|



#### **`playbook.yml`**  

```yaml
---
- name: Import Content View
  hosts: localhost # Run from localhost, modules will excute with API to Satellite
  gather_facts: true

  vars:
    satellite_server_url: "satellite.local" # Connected Satellite FQDN
    satellite_username: "admin" # Example username
    satellite_password: "redhat123" # Example password
    satellite_organization: "home" # Satellite organization

  tasks:
    - name: INCLUDE_ROLE | import_content_library
      ansible.builtin.include_role:
        name: import_content_library
...
```

## Documentation

### Red Hat Satellite Collection

[Link](https://console.redhat.com/ansible/automation-hub/repo/published/redhat/satellite/)

#### Modules
- [redhat.satellite.content_import_library](https://console.redhat.com/ansible/automation-hub/repo/published/redhat/satellite/content/module/content_import_library/)
- [redhat.satellite.content_import_info](https://console.redhat.com/ansible/automation-hub/repo/published/redhat/satellite/content/module/content_import_info/)
