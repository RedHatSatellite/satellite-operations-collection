redhat.satellite_operations.metrics
=============================

Setup Performace Co-Pilot and Grafana to gather metrics of a Satellite installation.

This role is heavily based on the [performancecopilot.metrics](https://github.com/performancecopilot/ansible-pcp) collection.

Role Variables
--------------

* `satellite_metrics_url`: The URL of the OpenMetrics endpoint of Satellite, defaults to `https://{{ ansible_fqdn | default('localhost') }}/metrics`.
* `satellite_metrics_pcp_optional_agents`: The optional PCP agents to enable, defaults to `[apache, openmetrics, postgresql, redis]`.
* `satellite_metrics_grafana_enabled`: Whether or not Grafana should be installed and configured on the system, defaults to `true` on Red Hat family systems, and to `false` otherwise.
* `satellite_metrics_grafana_pmproxy_url`: The URL of the `pmproxy` service to be used as the Grafana datasource, defaults to `http://{{ ansible_fqdn | default('localhost') }}:44322`.

Example Playbooks
-----------------

```yaml
---
- hosts: all
  gather_facts: true
  roles:
    - metrics
```
