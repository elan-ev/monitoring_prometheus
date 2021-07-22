# Ansible Role for prometheus

![molecule](https://github.com/elan-ev/monitoring_loki/actions/workflows/molecule.yml/badge.svg)

Install the latest [prometheus](https://github.com/prometheus/prometheus) version with [ansible](https://docs.ansible.com/).
This role is the multi-os ansible equivalent of https://github.com/lkiesow/prometheus-rpm.

## Role Variables

You can specify which template files to use for your configuration.
The role installs the default configuration, which you will likely want to extend or change.
To pass your own configuration file, specify the path to the jinja template in the variable `prometheus_config_template`.

Additionally, an `.env`-file is installed that expands the command line arguments of how prometheus is called by systemd.
Here you can also pass your individual file via the variable `prometheus_env_file`, so you are not limited to these values.

## Example Playbook

Just add the role to your playbook:

```yaml
- hosts: all
  become: true
  roles:
    - elan.monitoring_prometheus
```

## Development

For development and testing you can use [molecule](https://molecule.readthedocs.io/en/latest/).
With podman as driver you can install it like this – preferably in a virtual environment (if you use docker, substitute `podman` with `docker`):

```bash
pip install -r .dev_requirements.txt
```

Then you can *create* the test instances, apply the ansible config (*converge*) and *destroy* the test instances with these commands:

```bash
molecule create
molecule converge
molecule destroy
```

If you want to inspect a running test instance use `molecule login --host <instance_name>`, where you replace `<instance_name>` with the desired value.

## License

[BSD-3-Clause](LICENSE)

## Author Information

[ELAN e.V](https://elan-ev.de/)
