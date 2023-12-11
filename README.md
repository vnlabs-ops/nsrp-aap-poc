# nsrp-aap-poc

For Aruba switches
----------------

The variables that should be defined in your inventory for your AOS-Switch host are:

* `ansible_host`: IP address of switch in `A.B.C.D` format. For IPv6 hosts use a string and enclose in square brackets E.G. `'[2001::1]'` 
* `ansible_user`: Username for switch in `plaintext` format  
* `ansible_password`: Password for switch in `plaintext` format  
* `ansible_connection`: Set to local to use REST API modules, and to network_cli to use SSH/CLI modules
    See below for info on using both REST API modules and SSH/CLI modules on a host
* `ansible_network_os`: Must always be set to `arubanetworks.aos_switch.arubaoss`  

### Sample Inventory:

#### YAML

```yaml
all:
  hosts:
    aosswitch_1:
      ansible_host: 10.0.0.1
      ansible_user: admin
      ansible_password: password
      # local --> REST API connection method
      # network_cli: SSH/CLI connection mode
      ansible_connection: local  
      ansible_network_os: arubanetworks.aos_switch.arubaoss  # Do not change
```

Setting Environment Variables
--------------
In order to use the AOS-Switch collection you need to modify your environment in order for Ansible to recognize the Network OS:  

Example of setting environment variable in the command :
 `$ ANSIBLE_NETWORK_GROUP_MODULES=arubaoss  ansible-playbook sample_playbook.yml -i inventory.yml`   

 You can also check which ansible.cfg is used by increasing the verbosity (add -v to command above) and accordingly set the value of NETWORK_GROUP_MODULES to "arubaoss" in the [defaults] section.
```
[defaults]
NETWORK_GROUP_MODULES=arubaoss
```   