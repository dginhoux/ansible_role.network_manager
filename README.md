Ansible Role : dginhoux.network_manager
=========

This ansible role configure network connections with NetworkMaanger


Requirements
------------

This role require a supported platform defined in `meta/main.yml`.
It will skip node with unsupported platform ; this behaviour can be bypassed by settings this variable `asserts_bypass=True`.


Role Variables
--------------

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

network_manager_conf_d: []
# network_manager_conf_d:
#   - name: plugin-ifcfg-rh
#     cfg:
#       main:
#         plugins: ifcfg-rh
```



Dependencies
------------

none


Example Playbook
----------------



License
-------

BSD


Author Information
------------------

https://github.com/dginhoux/
