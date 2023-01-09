redhat.satellite_operations.backup
============================

Sets up backup cronjob using `satellite_maintain`, creating one full backup each Sunday and incremental ones otherwise.

Role Variables
--------------

* `satellite_backup_destination`: Destination where to write the backups to, defaults to `/var/backup/foreman`
* `satellite_backup_type`: Backup type, can be either `online` or `offline`, defaults to `online`
* `satellite_backup_keep_full`: How many full (weekly) backups to keep, defaults to `2`

None

Example Playbooks
-----------------

```yaml
---
- hosts: all
  gather_facts: true
  roles:
    - backup
```
