# Grafana Standalone for YunoHost

<!-- [![Integration level](https://dash.yunohost.org/integration/grafana.svg)](https://dash.yunohost.org/appci/app/grafana) ![Working status](https://ci-apps.yunohost.org/ci/badges/grafana.status.svg) ![Maintenance status](https://ci-apps.yunohost.org/ci/badges/grafana.maintain.svg) -->
<!-- [![Install Grafana with YunoHost](https://install-app.yunohost.org/install-with-yunohost.svg)](https://install-app.yunohost.org/?app=grafana) -->

*[Lire ce readme en français.](./README_fr.md)*

> *This package allows you to install Grafana quickly and simply on a YunoHost server.
If you don't have YunoHost, please consult [the guide](https://yunohost.org/#/install) to learn how to install it.*

## Overview

Metric & analytic dashboards for monitoring

**Shipped version:** 9.3.2~ynh1

**Demo:** https://play.grafana.org

## Screenshots

![Screenshot of Grafana](https://grafana.com/api/dashboards/1860/images/7994/image)

## Disclaimers / important information

 * This is a fork from the official [Grafana setup for YUNoHost](https://github.com/YunoHost-Apps/grafana_ynh)
 * This Grafana setup ships standalone, without any datasource pre-installed. You'll have to setup one, for instance Prometheus, InfluxDB or Netdata.

## Configuration

### Using With Prometheus

 * [Install Prometheus with YUNoHost](https://github.com/YunoHost-Apps/prometheus_ynh)
 * Install the node-exporter package `sudo apt install prometheus-node-exporter`
 * Configure Prometheus to Scrap the node exporter, by adding the following snippet under the prometheus config, then restart prometheus.

```yaml
# /opt/yunohost/prometheus/prometheus.yml
# ...
scrape_configs:
  # Keep the prometheus job...
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']
```
 * Add Prometheus as a datasource on Grafana. Be careful that if you have added `Prometheus` on a non root path of a domain, you'll need to use this path the datasource URL too. For instance the datasource prometheus address is `http://localhost:9100/prometheus` because Prometheus is installed under `myserver.com/prometheus`. 
 * You can now install an dashboard to view exported metrics, we recommend the excellent [Node Exporter Full](https://grafana.com/grafana/dashboards/1860-node-exporter-full) dashboard.
 * You can also define alerts on Grafana.

## Documentation

 * Official Grafana documentation: https://grafana.com/docs/grafana/latest/

## YunoHost specific features

* installs Grafana as dashboard server

#### Multi-users support

LDAP and HTTP auth are supported.

## Limitations

* The default dashboard may be updated in a further release of this package, so please make sure you create your own dashboards!
* Organizations creation doesn't play well with LDAP integration; it is disabled for standard users, but can't be disabled for administrators: **please do not create organizations**!

## Documentation and resources

* Official app website: <https://grafana.com/>
* Upstream app code repository: <https://github.com/grafana/grafana>
* Report a bug: <https://github.com/jlevesy/grafana_standalone_ynh/issues>

## Developer info

Please send your pull request to the [testing branch](https://github.com/jlevesy/grafana_standalone_ynh/tree/testing).

To try the testing branch, please proceed like that.

``` bash
sudo yunohost app install https://github.com/jlevesy/grafana_standalone_ynh/tree/testing --debug
or
sudo yunohost app upgrade grafana -u https://github.com/jlevesy/grafana_standalone_ynh/tree/testing --debug
```

**More info regarding app packaging:** <https://yunohost.org/packaging_apps>
