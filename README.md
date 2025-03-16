# Monitoring Pi

[![CI](https://github.com/DudeCalledBro/monitoring-pi/actions/workflows/ci.yml/badge.svg)](https://github.com/DudeCalledBro/monitoring-pi/actions/workflows/ci.yml)

This repository contains the Ansible code for deploying Uptime Kuma using Docker.

## Prerequisites

- Ensure you have Ansible installed (e.g. `pip3 install ansible`)
- Ensure Docker is installed on the monitoring server (you may want to checkout my [ansible-docker-role](https://github.com/DudeCalledBro/ansible-role-docker))

## Installation

1. Copy the example.hosts.yml file to hosts.yml. You also have to setup a variables file for your configuration. Therefore you have to copy example.config.yml to config.yml. Also have a look into the roles defaults.

2. Run the Ansible playbook to deploy uptime kuma

    ```bash
    ansible-playbook main.yml
    ```

> You may have to enter a password to SSH into the target system, so you need to add `-k` after the `ansible-playbook` command.

## Compose Override

You can define the variable `uptime_kuma_override` to override the compose services. This allows for customization of your Uptime Kuma deployment without modifying the original `compose.yaml` file.

Here's an example of how to use the override:

```yaml
uptime_kuma_override:
  services:
    monitoring:
      ports:
        - 3001:3001
```

In this example, we're overriding the ports, adding an environment variable, and specifying a custom volume for the uptime-kuma (monitoring) service.

For more information on how Docker Compose handles multiple files and overrides, please refer to the official Docker documentation on [multiple Compose files](https://docs.docker.com/compose/how-tos/multiple-compose-files/extends/#multiple-compose-files).

## License

Copyright © 2025 Niclas Spreng

Licensed under the [MIT license](LICENSE).
