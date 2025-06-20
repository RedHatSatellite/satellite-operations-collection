=========================================
redhat.satellite_operations Release Notes
=========================================

.. contents:: Topics

v3.0.1
======

Bugfixes
--------

- cloud_connector role - Remove protocol from NO_PROXY var (https://issues.redhat.com/browse/SAT-34224)

v3.0.0
======

Minor Changes
-------------

- cloud_connector role - Remove receptor cleanup steps in configure cloud connector
- cloud_connector role - Restart rhcd after writing out config file
- metrics role - new role to setup PCP integration with Foreman 3.9 and newer

v2.1.0
======

v2.0.0
======

Minor Changes
-------------

- cloud_connector role - don't mark proxy.conf systemd drop-in word-inaccessible, there is no benefit and systemd warns about this (https://bugzilla.redhat.com/show_bug.cgi?id=2169682)

v1.3.0
======

Minor Changes
-------------

- new role to configure backups using ``foreman-maintain``

Bugfixes
--------

- cloud_connector role - Ensure ``rhcd.service`` starts after system reboots
- fix paths in execution-environment.yml (https://bugzilla.redhat.com/show_bug.cgi?id=2156941)

v1.2.3
======

Bugfixes
--------

- cloud_connector role - use correct hostname variable when talking to console.redhat.com

v1.2.2
======

Bugfixes
--------

- cloud_connector role - use a regular expression to parse the CN from the cert

v1.2.1
======

Bugfixes
--------

- fix parsing of openssl certificate subject for EL7 and EL8

v1.2.0
======

Minor Changes
-------------

- add HTTP proxy support for cloud connector

v1.1.1
======

Bugfixes
--------

- update FORWARDER_URL for cloud connector

v1.1.0
======

Minor Changes
-------------

- cloud_connector - new role for installing Cloud Connector (https://github.com/theforeman/foreman-operations-collection/pull/85)

v1.0.2
======

Bugfixes
--------

- installer role - don't fail execution in check mode

v1.0.1
======

Bugfixes
--------

- correct collection metadata, so it can be uploaded to Galaxy

v1.0.0
======

Release Summary
---------------

This is the first stable release of the ``redhat.satellite_operations`` collection.

v0.3.0
======

v0.2.0
======

v0.1.0
======
