# Red Hat Satellite Operations Collection

## Description

Ansible assets for managing Satellite operations such as install or maintenance tasks.

## Requirements

* None

## Installation

Before using this collection, you need to install it, either directly from Automation Hub or via RPMs provided by Red Hat.

The GitHub repository serves as the source for the release and should not be used for direct installation and consumption of the collection.

### Installation from Automation Hub

To install it with the Ansible Galaxy command-line tool:

```
ansible-galaxy collection install redhat.satellite_operations
```

You can also include it in a requirements.yml file and install it with `ansible-galaxy collection install -r requirements.yml`, using the format:


```yaml
collections:
  - name: redhat.satellite_operations
```

To upgrade the collection to the latest available version, run the following command:

```
ansible-galaxy collection install redhat.satellite_operations --upgrade
```

You can also install a specific version of the collection. Use the following syntax to install version 1.0.0:

```
ansible-galaxy collection install redhat.satellite_operations:==1.0.0
```

See [using Ansible collections](https://docs.ansible.com/ansible/devel/user_guide/collections_using.html) for more details.

### Installation via RPM

The collection is also available as `ansible-collection-redhat-satellite_operations` in the Satellite repository.


## Testing

This collection is tested against all currently maintained Ansible versions and with all currently supported (by Ansible on the target node) Python versions.
You can find the list of maintained Ansible versions and their respective Python versions on [docs.ansible.com](https://docs.ansible.com/ansible/devel/reference_appendices/release_and_maintenance.html).

## Contributing

This collection is based on the [`theforeman.operations`](https://github.com/theforeman/foreman-operations-collection) community collection for Foreman and Katello.
If possible, any contributions should go directly to `theforeman.operations` from where they will flow back into this collection.


## Support

As Red Hat Ansible Certified Content, this collection is entitled to support through the Ansible Automation Platform (AAP) using the **Create issue** button on the top right corner.
If a support case cannot be opened with Red Hat and the collection has been obtained either from Galaxy or GitHub, there may community help available on the [Ansible Forum](https://forum.ansible.com/).


## Release Notes and Roadmap

Please see the [changelog](https://github.com/RedHatSatellite/satellite-operations-collection/blob/master/CHANGELOG.rst).


## Related Information

The official Satellite documentation can be found in the [Product Documentation section of the Red Hat Customer Portal](https://docs.redhat.com/en/documentation/red_hat_satellite/).


## License Information

This collection is licensed under the [GNU GPL v3](https://github.com/RedHatSatellite/satellite-operations-collection/blob/master/LICENSE).
