robedevops.varnish_from_epel
=========

This role install varnish from epel-release repository. This solution configures the **varnish.params** files based on the variables defined in the **default.yml** file.

Requirements
------------

N/A

Role Variables
--------------

Used as vcl version used for varnish. When install varnish from repository is really old.

```yaml 
varnish_vcl_version: 4.0
```

This define the home configuration for all varnish files
```yaml
varnish_home: /etc/varnish
```

Default configuration used by varnish. It can be changed here and the changes will be reflected in varnish.params files. Need to change also the playbook tasks.

```yaml
varnish_vcl_config: default.vcl
```

Define the address and port bind to the varnish process. The address is set using the ansible fact for ip address as dynamic solution but it can be set manually.

```yaml
varnish_listen_address: "{{ hostvars['varnish']['ansible_default_ipv4']['address'] }}"
varnish_listen_port: 6081
```

The Admin interface listen address and port are set as default. Any value can be used here but set this thinking about security risks.

```yaml
varnish_admin_listen_address: 127.0.0.1
varnish_admin_listen_port: 6082
```

All this configurations are self-explained. The most important one is the related with memory allocation and it can be set based on your resources.

```yaml

varnish_secret_file: secret
varnish_storage: "malloc,256M"
varnish_user: varnish
varnish_group: varnish
```

Dependencies
------------

N/A

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: varnish-cache
  gather_facts: yes
  become: yes
  roles:
      - { role: rodebdevops.varnish_from_epel }
```

Example of inventory
-------------------

Change this inventory with your values

```
varnish ansible_host=your_host_ip_or_name

[all:vars]
ansible_connection=ssh
ansible_user=centos
ansible_ssh_common_args='-o StrictHostKeyChecking=no'
ansible_ssh_private_key_file=/path/to/key.pem
```

License
-------

BSD

Author Information
------------------

Roberto Cardenas Isla - email: rcardenas20@gmail.com
