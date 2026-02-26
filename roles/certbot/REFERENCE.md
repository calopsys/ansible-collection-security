<!-- BEGIN_ANSIBLE_DOCS -->
# Ansible Role: calopsys.security.certbot
Version: 1.0.0

This role installs, manages and configures certbot on a Debian system.


## Requirements

| Platform | Versions |
| -------- | -------- |
| Debian | all |

## Role Arguments


### Entrypoint: main

Install and configure a certbot on Debian systems.

This role installs, manages and configures certbot on a Debian system.

|Option|Description|Type|Required|Default|
|---|---|---|---|---|
| calopsys_certbot_renew_timer_interval | Time for config time renew systemd. See https://www.freedesktop.org/software/systemd/man/latest/systemd.timer.html. This role uses OnUnitActiveSec. | str | no | 1w |
| calopsys_certbot_config_dir | The certbot base directory. | str | no | /etc/certbot |
| calopsys_certbot_venv_dir | The directory containing the certbot virtualenv. | str | no | {{ calopsys_certbot_config_dir }}/venv |
| calopsys_certbot_certificates | List of certificates to issue. | list of dicts of 'calopsys_certbot_certificates' options | yes |  |

#### Options for main > calopsys_certbot_certificates

|Option|Description|Type|Required|Default|
|---|---|---|---|---|
| name | Name of the certificate. | str | yes |  |
| config_template | The ini configuration template file. | str | yes |  |
| dns_pip_provider | Name of python plugin to download - required when using the DNS challenge. | str | no |  |
| dns_auth_template | Authentication configuration template file - required when using the DNS challenge. | str | no |  |
| hook_template | Deploy hook script template file for certificate renewal. | str | no |  |
| state | Certificate state. 'present' deploys config only, 'issued' ensures the cert exists, 'absent' removes config files. | str | no |  |

#### Choices for main > calopsys_certbot_certificates > state

|Choice|
|---|
| present |
| issued |
| absent |



## Dependencies
None.

## Example Playbook

```
- hosts: all
  tasks:
    - name: Importing role: calopsys.security.certbot
      ansible.builtin.import_role:
        name: calopsys.security.certbot
      vars:
        calopsys_certbot_certificates: # required, type: list of dicts of 'calopsys_certbot_certificates' options
```

## License

MIT

## Author and Project Information
Calopsys @ Calopsys

Issues: [tracker](https://github.com/calopsys/ansible-collection-security/issues)
<!-- END_ANSIBLE_DOCS -->
