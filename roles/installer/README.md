redhat.satellite_operations.installer
===============================

Run the satellite-installer

Role Variables
--------------

Required:

- `satellite_installer_scenario`: The installer scenario to run, this is required to be set. You can find the list of all scenario available by running `satellite-installer --list-scenarios` command.

Optional:

- `satellite_installer_package`: Package containing the installer scenario
- `satellite_installer_options`: Array of options to pass to the installer
- `satellite_installer_verbose`: Enables verbose output mode in the installer
- `satellite_installer_no_colors`: Disables color output from the installer
- `satellite_installer_command`: Installer command to run, can be used by derivative projects to specify a branded command
- `satellite_installer_locale`: Locale to run the installer with, this must not be ```C```, defaults to ```en_US.UTF-8```
- `satellite_installer_timeout`: Time allowed for installer to run before it is assumed failed, defaults to 30m

Example Playbooks
-----------------

Run the installer with the `satellite` scenario, setting the initial organization and admin password:

```yaml
- hosts: target-host
  roles:
    - role: redhat.satellite_operations.installer
      vars:
        satellite_installer_scenario: satellite
        satellite_installer_package: satellite-installer
        satellite_installer_options:
          - '--foreman-initial-organization "ACME Inc"'
          - '--foreman-initial-admin-password changeme'
```
