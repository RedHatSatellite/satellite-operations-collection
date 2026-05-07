# Satellite Capsule Install

## Description

This role will install and configure Red Hat Satellite Capsule Server with the option of default certificates, custom certificates, and loadbalancing behind HA Proxies

[Red Hat Satellite Capsules Documentation](https://access.redhat.com/documentation/en-us/red_hat_satellite/6.14/html/installing_capsule_server/index)

## Requirements

As specified in the [Red Hat Satellite Capsule Server Documentation](https://docs.redhat.com/en/documentation/red_hat_satellite/6.17/html/installing_capsule_server/preparing-environment-for-capsule-installation):

- Red Hat Enterprise Linux 9
- Ansible 2.9 or higher
- 4-core 2.0 GHz CPU at a minimum
- 12 GB RAM at a minimum
- Valid Red Hat Satellite Subscription
- Red Hat Satellite Infrastructure Subscription manifest

## Default Role Variables

Contains all variables in the [defaults variable file](defaults/main.yml) which verify OS configuration and storage requirements

|Variable Name|Default Value|Type|Description|Required|
|:---|:---:|:---:|:---|:---|
|`satellite_os_version`|9|string|Used to verify that the server is on the required RHEL version|yes|
|`satellite_server_basearch`|x86_64|string|The name of the default/main Organization on Satellite|yes|
|`satellite_min_cpu_count`|4|string|The name of the default/main Organization on Satellite|yes|
|`satellite_min_memory_size`|12288|string|The location to use for the Satellite server|yes|
|`capsule_data_disk_min_size`|500|boolean|Set true if the Satellite should be connected and sync from RHN, false if Satellite will be disconnected|yes|
|`capsule_min_pulp_size`|300|string|The timezone to set on the server at the OS level|yes|
|`capsule_min_pgsql_size`|20|string|The storage device to use|yes|
|`capsule_pulp_size`|1500g|string|The size, in GB, of the /var/lib/pulp directory|yes|
|`capsule_pgsql_size`|150g|string|The size, in GB, of the /var/lib/pgsql directory|yes|
|`capsule_data_device`|/dev|string|The storage device to use|yes|
|`capsule_vg_name`|cap_vg01|string|The name of the volume group used for Capsule storage|yes|
|`capsule_req_dirs`|See defaults variable file for default value|list of dictionaries|Each entry specifies a mount point, a logical volume name, and a logical volume size|yes|
|`satellite_capsule_packages`|See defaults variable file for default value|list|List of packages to install on the server|yes|
|`satellite_installer_scenario`|capsule|string|Scenario to use for the satellite-installer command|yes|

## Role Variables

Contains all variables in the [defaults variable file](defaults/main.yml) which are used to install and configure the Capsule Server

|Variable Name|Default Value|Type|Description|Required|
|:---|:---:|:---:|:---|:---|
|`satellite_admin_username`|admin|string|Username for the Satellite admin user|yes|
|`satellite_admin_password`||string|Password for the Satellite admin user|yes|
|`satellite_capsule_organization`||string|The name of the default/main Organization on Satellite|yes|
|`satellite_capsule_ak`||string|The activation key to use for registration|yes|
|`satellite_capsule_location`||string|The Location that the Capsule will be in|yes|
|`satellite_fqdn`||string|The disconnected Satellite to register the Capsule to|yes|
|`satellite_capsule_sync_wait_time`|86400|integer|The amount of time in seconds for Ansible to wait for the initial Capsule sync to finish|yes|
|`satellite_haproxy`|false|boolean|Set to true if loadbalancing is desired|yes|
|`satellite_loadbalancer_fqdn`||string|The FQDN of the loadbalancer|no|
|`satellite_loadbalancer_ak`||string|Activation key used to register the loadbalancer to Satellite|no|
|`satellite_loadbalancer_ports`|See vars file for default values|list|Required ports to open on the loadbalancer|no|
|`satellite_installer_options`|See defaults variable file for default value|list of dictionaries|Options to pass into the satellite-installer command|yes|
|`satellite_capsule_lifecycle_envs`|See defaults variable file for default value|list|Lifecycle Environments that the Capsule will sync to|yes|

## Dependencies

- Capsule Server must be installed on a freshly provisioned system that serves no other function except to run Capsule Server. The freshly provisioned system must not have the following users provided by external identity providers to avoid conflicts with the local users that Capsule Server creates:
  - apache
  - foreman-proxy
  - postgres
  - pulp
  - puppet
  - redis
- Collections located in [collections/requirements.yml](collections/requirements.yml) must be installed

## Example Playbooks

```yaml
---
- name: Install and configure Red Hat Satellite Capsule Server
  hosts: capsule.example.com
  tasks:
    - name: Include install role
      ansible.builtin.include_role:
        name: capsule_automation_install
...
