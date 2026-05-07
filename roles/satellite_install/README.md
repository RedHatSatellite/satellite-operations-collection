# Satellite Install

## Description

This role will install and configure Red Hat Satellite with the option of either a connected environment or a disconnected environment

## Requirements

As specified in the [Red Hat Satellite Documentation](https://docs.redhat.com/en/documentation/red_hat_satellite):

- Red Hat Enterprise Linux 9
- Ansible 2.9 or higher
- 4-core 2.0 GHz CPU at a minimum
- 20 GB RAM at a minimum
- Valid Red Hat Satellite Subscription
- Red Hat Satellite Infrastructure Subscription manifest

## Common Variables

Contains all variables in the [defaults](defaults/main/main.yml) variable file, as well as a few variables that are in both the [connected](defaults/main/connected.yml) and the [disconnected](defaults/main/disconnected.yml) variable files. Since they are common, they are likely set to the same value for both connected and disconnected (with the exception of satellite_rhn_connected)

|Variable Name|Default Value|Type|Description|Required|
|:---|:---:|:---:|:---|:---|
|`satellite_admin_username`|admin|string|Username for the Satellite admin user|yes|
|`satellite_admin_password`|""|string|Password for the Satellite admin user|yes|
|`satellite_server_url`|https://{{ ansible_fqdn }}|string|URL of the Satellite server is the hostname|yes|
|`satellite_organization`||string|The name of the default/main Organization on Satellite|yes|
|`satellite_initial_location`||string|The location to use for the Satellite server|yes|
|`satellite_rhn_connected`|true|boolean|Set true if the Satellite should be connected and sync from RHN, false if Satellite will be disconnected|yes|
|`satellite_timezone`|UTC|string|The timezone to set on the server at the OS level|yes|
|`satellite_data_device`|/dev|string|The storage device to use|yes|
|`satellite_validate_certs`|false|boolean|Whether or not to validate certificates during module use and API calls|yes|
|`satellite_min_cpu_count`|4|integer|Minimum number of cores required|yes|
|`satellite_min_memory_size`|20240|integer|Minimum amount of RAM (in MB) required|yes|
|`satellite_data_disk_min_size`|500|integer|Minimum amount of storage (in GB) required by the disk|yes|
|`satellite_min_pulp_size`|300|integer|Minimum amount of storage (in GB) required by the /var/lib/pulp directory|yes|
|`satellite_min_pgsql_size`|20|integer|Minimum amount of storage (in GB) required by the /var/lib/pgsql directory|yes|
|`satellite_server_basearch`|x86_64|string|Used to verify that the server is on x86_64 architecture as required|yes|
|`satellite_os_version`|9|string|Used to verify that the server is on the required RHEL version|yes|
|`satellite_deployment_version`|6.17|string|The latest major version of Satellite, used to enable the correct version of Red Hat repositories|yes|
|`satellite_email`||string|Administrator email to set for the Satellite server|no|
|`satellite_giturl`||string|Optional Git URL to set on the Satellite server|no|
|`satellite_pulp_size`|1500g|string|The size, in GB, of the /var/lib/pulp directory|yes|
|`satellite_pgsql_size`|150g|string|The size, in GB, of the /var/lib/pgsql directory|yes|
|`satellite_req_dirs`|See variable files for default value|list of dictionaries|Each entry specifies a mount point, a logical volume name, and a logical volume size|yes|
|`satellite_vg_name`|vg_rhsat|string|The name of the volume group used for Satellite storage|yes|
|`satellite_selinux_state`|enforcing|string|State of SELinux|yes|
|`satellite_installer_scenario`|satellite|string|Scenario to use with satellite-installer command|yes|
|`satellite_installer_options`|See variable files for default value|list|Options to pass into the satellite-installer command|yes|
|`satellite_settings`|See variable files for default value|list of dictionaries|Various Satellite settings|yes|
|`satellite_repo_sync_wait_time`|21600|integer|The amount of time, in seconds, to wait for the initial repository syncs to finish|yes|
|`satellite_syncplan_interval`|daily |string|The interval at which the sync plan will run. Can be set to hourly, daily, weekly, or a custom cron value|yes|
|`satellite_subscription_to_search`|Red Hat Satellite Infrastructure Subscription|string|The Red Hat Subscription to search for to ensure a valid manifest is present|yes|
|`satellite_packages`|See variable files for default value|list|Packages to install on Satellite server|yes|
|`satellite_size`|See variable files for default value|list of dictionaries|Used to determine which tuning profile to apply during installation|yes|

## Connected Satellite Variables

These variables are specific to a connected Satellite environment installation, meaning that the variable is either absent in a disconnected Satellite environment, or set to a different value

|Variable Name|Default Value|Type|Description|Required|
|:---|:---:|:---:|:---|:---|
|`satellite_rhn_org`||string|Red Hat Organization ID to use when registering the Satellite Server|yes|
|`satellite_rhn_activation_key`||string|Red Hat Activation Key to use when registering the Satellite Server|yes|
|`satellite_manifest_path`||string|The full path to the manifest file located on the connected Satellite server - recommended to place somewhere on /root|yes|
|`satellite_ak`|satellite6-satinfra|string|The name of the activation key used for the Satellite content view. Also used to register the disconnected Satellite. See disconnected vars below|yes|
|`satellite_sync_time`|16:30:00|string|The time at which the defined sync plan will run|yes|
|`satellite_redhat_repos`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Red Hat Repositories to enable post-installation|yes|
|`satellite_content_credentials`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Content Credentials to create post-installation. The 'content' key contains the public URL to the GPG key|yes|
|`satellite_products`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Products to create post-installation. The 'url' key contains the public URL to the repository|yes|
|`satellite_lifecycle_envs`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Lifecycle Environments to create post-installation|yes|
|`satellite_content_views`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Content Views to create post-installation. Note the difference in structure for a regular Content View vs a Composite Content View|yes|
|`satellite_activation_keys`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Activation Keys to create post-installation|yes|
|`satellite_locations`|See variable file for default value|list of dictionaries|Locations to create post-installation. Note that the 'parent' can be specified to create sub-locations|yes|

## Disconnected Satellite Variables

|Variable Name|Default Value|Type|Description|Example|
|:---|:---:|:---:|:---|:---|
|`satellite_disconnected_manifest_path`||string|The full path to the manifest file located on the disconnected Satellite server - recommended to place somewhere on /root|yes|
|`satellite_connected_fqdn`||string|The FQDN of the upstream connected Satellite that the disconnected Satellite will sync content from|yes|
|`satellite_ak`|satellite6-satinfra|string|The name of the activation key used to register the disconnected Satellite to the connected Satellite|yes|
|`satellite_capsule_ak`|capsule6-satinfra|string|The FQDN of the upstream connected Satellite that the disconnected Satellite will sync content from|yes|
|`satellite_sync_time`|19:30:00|string|The time at which the defined sync plan will run. Recommended to run a few hours after the connected Satellite sync plan to allow for the connected sync to finish|yes|
|`satellite_redhat_repos`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Red Hat Repositories to enable post-installation|yes|
|`satellite_content_credentials`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Content Credentials to create post-installation. The 'content' key contains the public URL to the GPG key|yes|
|`satellite_products`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Products to create post-installation. The 'url' key contains the public URL to the repository|yes|
|`satellite_lifecycle_envs`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Lifecycle Environments to create post-installation|yes|
|`satellite_content_views`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Content Views to create post-installation. Note the difference in structure for a regular Content View vs a Composite Content View|yes|
|`satellite_activation_keys`|See variable file for default value. Also see example below as this variable is complex|list of dictionaries|Activation Keys to create post-installation|yes|
|`satellite_locations`|See variable file for default value|list of dictionaries|Locations to create post-installation. Note that the 'parent' can be specified to create sub-locations|yes|

### Variable Example - satellite_redhat_repos

```yaml
satellite_redhat_repos:
  - name: "Red Hat Satellite Capsule {{ satellite_deployment_version }} for RHEL {{ ansible_distribution_major_version }} x86_64 (RPMs)"
    label: "satellite-capsule-{{ satellite_deployment_version }}-for-rhel-{{ ansible_distribution_major_version }}-x86_64-rpms"
    all: "true"
  - name: "Red Hat Satellite Maintenance {{ satellite_deployment_version }} for RHEL {{ ansible_distribution_major_version }} x86_64 (RPMs)"
    label: "satellite-maintenance-{{ satellite_deployment_version }}-for-rhel-{{ ansible_distribution_major_version }}-x86_64-rpms"
    all: "true"
  - name: "Red Hat Satellite {{ satellite_deployment_version }} for RHEL {{ ansible_distribution_major_version }} x86_64 (RPMs)"
    label: "satellite-{{ satellite_deployment_version }}-for-rhel-{{ ansible_distribution_major_version }}-x86_64-rpms"
    all: "true"
  - name: "Red Hat Satellite Client 6 for RHEL 9 x86_64 RPMs"
    label: "satellite-client-6-for-rhel-9-x86_64-rpms"
    all: "true"
  - name: "Red Hat Enterprise Linux 9 for x86_64 - BaseOS (RPMs)"
    label: rhel-9-for-x86_64-baseos-rpms
    repos:
      - releasever: "9"
    all: "false"
  - name: "Red Hat Enterprise Linux 9 for x86_64 - AppStream (RPMs)"
    label: rhel-9-for-x86_64-appstream-rpms
    repos:
      - releasever: "9"
    all: "false"
```

### Variable Example - satellite_content_credentials

```yaml
satellite_content_credentials:
  - name: RPM-GPG-KEY-EPEL
    content_type: gpg_key
    content: "{{ lookup('url', 'https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL', split_lines=False) }}"
  - name: RPM-GPG-KEY-EPEL9
    content_type: gpg_key
    content: "{{ lookup('url', 'https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-9', split_lines=False) }}"
```

### Variable Example - satellite_products

```yaml
satellite_products:
  - name: EPEL
    gpg_key: RPM-GPG-KEY-EPEL
    repositories:
      - name: EPEL9_X86
        content_type: yum
        gpg_key: RPM-GPG-KEY-EPEL9
        url: https://dl.fedoraproject.org/pub/epel/9/Everything/x86_64/
```

### Variable Example - satellite_lifecycle_envs

```yaml
satellite_lifecycle_envs:
  - name: satellite_lifecycle_capsule
    env_name: "satinfra"
    prior: "Library"
  - name: satellite_lifecycle_daily
    env_name: "daily"
    prior: "Library"
  - name: satellite_lifecycle_certify
    env_name: "certify"
    prior: "Library"
  - name: satellite_lifecycle_monthly
    env_name: "monthly"
    prior: "certify"
```

### Variable Example - satellite_content_views

```yaml
satellite_content_views:
  - name: satellite6
    repositories:
      - name: "Red Hat Enterprise Linux 9 for x86_64 - AppStream RPMs 9"
        product: "{{ satellite_rhel_product_name }}"
      - name: "Red Hat Enterprise Linux 9 for x86_64 - BaseOS RPMs 9"
        product: "{{ satellite_rhel_product_name }}"
      - name: "Red Hat Satellite Maintenance {{ satellite_deployment_version }} for RHEL 9 x86_64 RPMs"
        product: "{{ satellite_rhel_product_name }}"
      - name: "Red Hat Satellite {{ satellite_deployment_version }} for RHEL 9 x86_64 RPMs"
        product: "{{ satellite_satellite_product_name }}"
    lifecycle_environments: "{{ satellite_lifecycle_envs | selectattr('name', 'match', 'satellite_infra') | map(attribute='env_name') }}"
  - name: epel8_x86
    repositories:
      - name: 'EPEL8_X86'
        product: "{{ satellite_epel_product_name }}"
    lifecycle_environments: Library
  - name: epel9_x86
    repositories:
      - name: 'EPEL9_X86'
        product: "{{ satellite_epel_product_name }}"
    lifecycle_environments: Library
  - name: rhel8_epel_x86
    components:
      - content_view: rhel8_x86
        latest: true
      - content_view: epel8_x86
        latest: true
    lifecycle_environments:
      - "{{ satellite_lifecycle_envs | selectattr('name', 'match', 'satellite_lifecycle_daily') | map(attribute='env_name') | join(', ') }}"
      - "{{ satellite_lifecycle_envs | selectattr('name', 'match', 'satellite_lifecycle_certify') | map(attribute='env_name') | join(', ') }}"
      - "{{ satellite_lifecycle_envs | selectattr('name', 'match', 'satellite_lifecycle_monthly') | map(attribute='env_name') | join(', ') }}"
```

### Variable Example - satellite_activation_keys

```yaml
satellite_activation_keys:
  - name: satellite6-satinfra
    lifecycle_environment: "{{ satellite_lifecycle_envs | selectattr('name', 'match', 'satellite_infra') | map(attribute='env_name') | join(', ') }}"
    content_view: satellite6
    content_overrides:
      - label: rhel-9-for-x86_64-baseos-rpms
        override: enabled
      - label: rhel-9-for-x86_64-appstream-rpms
        override: enabled
      - label: "satellite-{{ satellite_deployment_version }}-for-rhel-9-x86_64-rpms"
        override: enabled
      - label: "satellite-maintenance-{{ satellite_deployment_version }}-for-rhel-9-x86_64-rpms"
        override: enabled
    service_level: "Premium"
  - name: capsule6-satinfra
    lifecycle_environment: "{{ satellite_lifecycle_envs | selectattr('name', 'match', 'satellite_lifecycle_capsule') | map(attribute='env_name') | join(', ') }}"
    content_view: capsule6
    content_overrides:
      - label: rhel-9-for-x86_64-baseos-rpms
        override: enabled
      - label: rhel-9-for-x86_64-appstream-rpms
        override: enabled
      - label: "satellite-capsule-{{ satellite_deployment_version }}-for-rhel-9-x86_64-rpms"
        override: enabled
      - label: "satellite-maintenance-{{ satellite_deployment_version }}-for-rhel-9-x86_64-rpms"
        override: enabled
    service_level: "Premium"
```

## Dependencies

- Satellite Server must be installed on a freshly provisioned system that serves no other function except to run Satellite Server. The freshly provisioned system must not have the following users provided by external identity providers to avoid conflicts with the local users that Satellite Server creates:
  - apache
  - foreman
  - foreman-proxy
  - postgres
  - pulp
  - puppet
  - redis
  - tomcat
- Collections located in [collections/requirements.yml](collections/requirements.yml) must be installed

## Example Playbooks

```yaml
---
- name: Install and configure Red Hat Satellite
  hosts: satellite.example.com
  tasks:
    - name: Include install role
      ansible.builtin.include_role:
        name: satellite_automation_install
...
```

## TODO AAP vs CLI execution differences

## License

[GPLv3](LICENSE)

## Author Information

Cory McKee <cmckee@redhat.com>

Bryce Tant <btrant@redhat.com>
