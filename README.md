networkmanager
==============

Role which helps to install and configure NetworkManager.

The configuration of the role is done in such way that it should not be necessary
to change the role for any kind of configuration. All can be done either by
changing role parameters or by declaring completely new configuration as a
variable. That makes this role absolutely universal. See the examples below for
more details.

Please report any issues or send PR.


Example
-------

```yaml
---

- name: Default installation
  hosts: myhost1
  roles:
    - networkmanager

- name: Example of how to change configuration for NetworkManager
  hosts: myhost1
  vars:
    # Disable resolv.conf overwriting
    networkmanager_config_main:
      dns: none
  roles:
    - networkmanager
```


Role variables
--------------

List of variables used by the role:

```yaml
# Package to be installed (you can force a specific version here)
networkmanager_pkg: NetworkManager

# Default service name
networkmanager_service: NetworkManager

# Default location of the networkmanager.conf file
networkmanager_conf_file: /etc/NetworkManager/NetworkManager.conf


# Default list of options for the main section
networkmanager_config_main: {}

# Default list of options for the logging section
networkmanager_config_logging: {}

# Default configuration
networkmanager_config_default:
  main: "{{ networkmanager_config_main }}"
  logging: "{{ networkmanager_config_logging }}"

# Custom configuration
networkmanager_config_custom: {}

# Final configuration
networkmanager_config: "{{
  networkmanager_config_default | combine(
  networkmanager_config_custom) }}"
```


Dependencies
------------

- [`config_encoder_filters`](https://github.com/jtyr/ansible-config_encoder_filters)


License
-------

MIT


Author
------

Jiri Tyr
