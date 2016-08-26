# Ansible Role: OAuth2 Proxy

This role will deal with the setup and config of [oauth2-proxy](https://github.com/bitly/oauth2_proxy).

It's part of the Manala <a href="http://www.manala.io" target="_blank">Ansible stack</a> but can be used as a stand alone component.

## Requirements

This role is made to work with the __manala__ oauth2-proxy debian package, available on the __manala__ debian repository. Please use the [**manala.apt**](https://galaxy.ansible.com/manala/apt/) role to handle it properly.

```yaml
manala_apt_preferences:
 - oauth2-proxy@manala
```

## Dependencies

None.

## Installation

### Ansible 2+

Using ansible galaxy cli:

```bash
ansible-galaxy install manala.oauth2-proxy
```

Using ansible galaxy requirements file:

```yaml
- src: manala.oauth2-proxy
```

## Role Handlers

| Name                   | Type    | Description          |
| ---------------------- | ------- | -------------------- |
| `oauth2 proxy restart` | Service | Restart oauth2 proxy |

## Role Variables

| Name                                  | Default                      | Type   | Description          |
| ------------------------------------- | ---------------------------- | ------ | -------------------- |
| `manala_oauth2_proxy_config_file`     | /etc/oauth2-proxy/config.cfg | String | Config file          |
| `manala_oauth2_proxy_config_template` | ~                            | String | Config template      |
| `manala_oauth2_proxy_config`          | []                           | Array  | Config               |

### Configuration example

```yaml
manala_oauth2_proxy_config:
  - http_address: 0.0.0.0:80
  - request_logging: true
  - upstreams:
    - http://127.0.0.1:8080/
  - email_domains:
    - manalas.com
  - client_id: oauth2_client_id
  - client_secret: oauth2_client_secret
  - cookie_name: _oauth2_proxy
  - cookie_secret: cookie_secret
  - cookie_domain: .manalas.com
  - cookie_expire: 168h
  - cookie_refresh: 1h
  - cookie_secure: true
  - cookie_httponly: true
  - skip_auth_regex:
    - /foo
```

## Example playbook

```yaml
- hosts: servers
  roles:
    - { role: manala.oauth2-proxy }
```

# Licence

MIT

# Author information

Manala [**(http://www.manala.io/)**](http://www.manala.io)
