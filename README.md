# Ansible Role - OpenWISP Dockerized

Based on the official [OpenWISP Docker images](https://github.com/openwisp/docker-openwisp).

This role strips some of the containers like `postfix` and `openvpn`. You can add them yourself if needed - see [original docker-compose.yml](https://github.com/openwisp/docker-openwisp/blob/master/docker-compose.yml)

----

## Config

See [the defaults](https://github.com/NiceRath/ansible-openwisp-dockerized/blob/main/defaults/main.yml) for all options.

By default, the data will be saved to `/var/local/`

```yaml
openwisp:
  secrets:
    django: !vault |
      ...
    db: !vault |
      ...

  settings:
    domain: 'wlan.template.niceshops.com'
    domain_api: 'wlan-api.template.niceshops.com'
    email: 'wlan@template.niceshops.com'

  manage:
    docker: true  # disable to self-manage docker setup
```

You might want to use 'ansible-vault' to encrypt the secrets: `ansible-vault encrypt_string 'YOUR-SECRET'`

You may also want to update some additional [environmental variables](https://github.com/NiceRath/ansible-openwisp-dockerized/blob/main/templates/etc/openwisp/env.j2).

----

## Run

```bash
ansible-galaxy install -r requirements.yml
ansible-playbook -k -K -i inventories/xx/hosts.yml playbook.yml --limit wlan-srv -D
```
