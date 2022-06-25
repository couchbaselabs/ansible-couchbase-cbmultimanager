# cbmultimanager Ansible Role

[![License](https://img.shields.io/github/license/couchbaselabs/ansible-couchbase-exporter.svg)](https://www.apache.org/licenses/LICENSE-2.0)


## Description

Deploy [cbmultimanager](https://docs.couchbase.com/cmos/current/index.html) Couchbase Multi Cluster Manager


## Requirements

-   Ansible >= 2.10 (It might work on previous versions, but we cannot guarantee it)
-   jmespath on deployer machine. If you are using Ansible from a Python virtualenv, install _jmespath_ to the same virtualenv via pip.


## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.  The only values necessary to change would be the `couchbase_username` and `couchbase_password`.

| **Name**           | **Default Value** | **Description**                    |
| :-------------- | :------------- | :-----------------------------------|
| cbmultimanager_version | `0.3.0` | The version of cbmultimanager to install |
| cbmultimanager_user | `cbmultimanager` | The local OS user to run cbmultimanager as |
| cbmultimanager_user_group | `cbmultimanager` | The local OS user group |
| cbmultimanager_install_dir | `/opt/cbmultimanager/bin` | The path to the install directory |
| cbmultimanager_binary | `cbmultimanager` | The name of the binary |
| cbmultimanager_conf_dir | `/etc/cbmultimanager` | The configuration directory, contains an environment file |
| cbmultimanager_env_file | `service.env` | The name of the environment file |
| cbmultimanager_local_tmp_dir | `/tmp/cbmultimanager` | The temporary directory on the ansible controller to download the binary to |
| cbmultimanager_log_level | `debug` |  Set the log level, options are [error, warn, info, debug] |
| cbmultimanager_log_dir | `/var/log/cbmultimanager/` | The location to log too. If it does not exist it will try to create it. |
| cbmultimanager_data_dir | `/var/lib/cbmultimanager/` | The path to the data directory |
| cbmultimanager_sqlite_dbname | `data.sqlite` | The name of the sqlite database file |
| cbmultimanager_sqlite_password | `password` | The encryption key for the sqlite database |
| cbmultimanager_cert_path | `""` | Path to a PEM-encoded X.509 certificate to use to serve the API/UI over TLS. If the certificate is signed by a CA, this must also contain the full chain to the CA root certificate, including any intermediates. Can be omitted, in which case TLS serving will be disabled. |
| cbmultimanager_key_path | `""` | Path to a PEM-encoded private key for the certificate in cert-path. |
| cbmultimanager_admin_user | `admin` | The username to use when logging into the cbmultimanager UI |
| cbmultimanager_admin_password | `admin` | The password to use when logging into the cbmultimanager UI |
| cbmultimanager_log_check_lifetime | `1h` | How long will log alerts fire before being expired. |
| cbmultimanager_enable_admin_api | `true` |  Enable the admin REST API |
| cbmultimanager_enable_cluster_mgmt_api | `true` | Enable the extended REST API. |
| cbmultimanager_enable_extended_api | `true` | Enable the cluster management REST API |
| cbmultimanager_prometheus_url | `""` | Base URL of Prometheus instance used for auto-provisioning |
| cbmultimanager_prometheus_label_selector | `job=couchbase` | Prometheus label selector to use to discover Couchbase Server clusters. Syntax: label1=value label2=value |
| cbmultimanager_alertmanager_urls | `http://localhost:9093` | URLs of Alertmanager instances to send alerts to. This must contain the entire base URL, including http or https |
| cbmultimanager_alertmanager_resend_delay | `30m` | Interval between re-sending alerts to Alertmanager. |
| cbmultimanager_alert_manager_base_labels | `""` | Base labels to be applied to alerts for Alertmanager. Syntax: label1=value label2=value |
| couchbase_username | `Administrator` | Couchbase user name (only needed when using Prometheus discovery) |
| couchbase_password | `password` |  Couchbase password (only needed when using Prometheus discovery) |
| cbmultimanager_http_port | `7196` | The port to serve HTTP REST API |
| cbmultimanager_https_port | `7197` | The port to serve HTTPS REST API |


## Installation

You can install this role with the `ansible-galaxy` command, and can run it
directly from the git repository.

You should install it like this:

```
ansible-galaxy install git+https://github.com/couchbaselabs/ansible-couchbase-cbmultimanager.git
```

## Example

### Playbook

Use it in a playbook as follows:

```yaml
- hosts: all
  roles:
    - couchbaselabs.cbmultimanager
```

## Useful Commands

### Manage the Service

It may be necessary from time to time to start, stop, restart, or get the status of the `cbmultimanager` service.

```bash
sudo systemctl start cbmultimanager
sudo systemctl status cbmultimanager
sudo systemctl restart cbmultimanager
```

### Viewing Standard Out

Since the exporter writes to stdout for logging, those messages can be viewed through `journalctl`

##### Most Recent Messages

```bash
sudo journalctl -r -t cbmultimanager
```

##### Follow Messages

```bash
sudo journalctl -f -t cbmultimanager
```

## License

This project is provided as is with no support and is licensed under Apache 2.0. See [LICENSE](/LICENSE) for more details.
