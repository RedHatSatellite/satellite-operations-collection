redhat.satellite_operations.installer
=====================================

Run the satellite-installer

Role Variables
--------------

Required:

- `satellite_installer_scenario`: The installer scenario to run, this is required to be set

Optional:

- `satellite_installer_package`: Package containing the installer scenario
- `satellite_installer_options`: Array of options to pass to the installer
- `satellite_installer_verbose`: Enables verbose output mode in the installer
- `satellite_installer_no_colors`: Disables color output from the installer
- `satellite_installer_command`: Installer command to run, can be used by derivative projects to specify a branded command

Example Playbooks
-----------------

Run the installer setting the initial admin password:

```yaml
- hosts: target-host
  roles:
    - role: redhat.satellite_operations.installer
      vars:
        satellite_installer_options:
          - '--foreman-initial-admin-password changeme'
```
