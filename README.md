# ROLE dginhoux.network_manager



## DESCRIPTION

This ansible role configure network connections with NetworkMaanger.



## REQUIREMENTS

#### SUPPORTED PLATFORMS

This role require a supported platform.<br />
It will skip node with unsupported platform to avoid any compatibility problem.<br />
This behaviour can be bypassed by settings the following variable `asserts_bypass=True`.

| Platform | Versions |
|----------|----------|
| Debian | buster, bullseye |
| Fedora | 33, 34, 35, 36, 37, 38 |
| EL | 7, 8 |

#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.network_manager
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.network_manager dginhoux.network_manager
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.network_manager
      ansible.builtin.include_role:
        name: dginhoux.network_manager
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
network_manager_configure: "generate"
# network_manager_configure: "cleanup"

network_manager_cleanup_old_systems: true


## availables settings are listed here
# https://docs.ansible.com/ansible/latest/collections/community/general/nmcli_module.html
##
network_manager_connections:
  - conn_name: ens18
    state: present
    autoconnect: true
    dns4:
      - 192.168.175.10
      - 192.168.175.11
      - 192.168.175.12
      - 192.168.175.13
    dns6: []
    dns4_search:
      - infra.ginhoux.net
      - ginhoux.net
    dns6_search: []
    gw4: 192.168.175.254
    ip4:
      - 192.168.175.142/24
    ifname: ens18
    method4: manual
    method6: link-local
    type: ethernet

##
# https://people.freedesktop.org/~lkundrak/nm-docs/NetworkManager.conf.html
##
network_manager_conf:
  main:
    dns: none
    rc-manager: unmanaged
  logging:
    level: INFO


network_manager_conf_defaults:
  main:
    plugins: keyfile
  logging:
    level: WARN
    # domains: ALL

network_manager_conf_d: []
# network_manager_conf_d:
#   - name: plugin-ifcfg-rh
#     cfg:
#       main:
#         plugins: ifcfg-rh


network_manager_service_name: NetworkManager
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

* RedHat Family 

```yaml
network_manager_packages_list:
  - name: NetworkManager
    state: present
  - name: NetworkManager-initscripts-ifcfg-rh
    state: absent
```

* Debian Family 

```yaml
network_manager_packages_list:
  - name: network-manager
    state: present
```


## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
