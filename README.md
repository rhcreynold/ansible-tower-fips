Role Name
=========

An Ansible Playbook(s) to install Ansible Tower 3.4+ on a RHEL host with FIPS enabled.

Requirements
------------
Valid RHEL and Ansible Tower subscription.  You will need a base RHLE 7 system with ssh connectivity.  Add your access.redhat.com login to a vault file along with the password and the Pool name that contains the products needed.  Update main.yml for the vault file and add an ip to the inventory.

Role Variables
--------------

tower-vars.yml:

```yaml
disconnected: false
use_public_dns: true
dns_server_public: 8.8.8.8
register_rhn: true
tower:
  repos:
    - rhel-7-server-rpms
    - rhel-7-server-extras-rpms
    - rhel-7-server-ansible-2.6-rpms
rhn_user: "{{ vault_rhn_user }}"
rhn_pass: "{{ vault_rhn_pwd }}"
rhn_pool: "{{ vault_rhn_pool_name }}"
tower_pw: "{{ vault_tower_pwd }}"

```
vault.sample:
```yaml
#RHN Info
vault_rhn_user: rhnuser
vault_rhn_pwd: redhat
vault_rhn_pool_name: Subscription Pool Name
#Tower
vault_tower_pwd: redhat
```


Dependencies
------------

To install RHEL FIPS and Ansible Tower you need a valid RHEL and Ansible Tower subscription to enable the following repositories:

For RHEL 7:

- rhel-7-server-rpms
- rhel-7-server-extras-rpms
- rhel-7-server-ansible-2.6-rpms

Some of the roles come from: https://github.com/redhat-kejones/hattrick


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: tower
  become: yes
  vars_files:
    - 'tower-vars.yml'
    - 'vault.sample'
  roles:
    - rhel_common
    - ansible.fips
    - tower
```

License
-------

GPL

Author Information
------------------

https://github.com/rhcreynold
