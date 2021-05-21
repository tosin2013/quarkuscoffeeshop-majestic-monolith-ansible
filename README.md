quarkuscoffeeshop-majestic-monolith tower role
=========

quarkuscoffeeshop-majestic-monolith is an application that can be deployed using RHEL edge.  This repo uses the scripts created in [RHEL Edge Application collection](https://github.com/tosin2013/rhel-edge-application-collection). This tole will be used in ansible tower to deploy to instances.

Requirements
------------
* ansible.posix.sysctl
```
ansible-galaxy collection install ansible.posix
ansible-galaxy collection install containers.podman
```

The role swygue-redhat-subscription is required by this role to subscribe the system.
```
ansible-galaxy install git+https://github.com/Qubinode/swygue-redhat-subscription.git
```

To-do
-----
[ ] Still working on registration  
[ ] Deploy dev instance function via ansible tower. Deploy a development instance of [rhel-edge-application-collection](https://github.com/tosin2013/rhel-edge-application-collection) to target device.  
[ ] Deploy builder image to target rhel edge devices using [rhel-edge-automation-arch](https://github.com/redhat-cop/rhel-edge-automation-arch)  
[ ] Provision vms on different instances and push builder image?  
[ ] Test against smaller devices?

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    ---
    - hosts: rhel_edge_device
      remote_user: admin
      become: true
      vars: 
        rhsm_user: username@example.com
        rhsm_password: Y0uRp@sSw0rd
        external_endpoint: 192.168.1.10
      roles:
        - quarkuscoffeeshop-majestic-monolith-ansible

License
-------

BSD

Author Information
------------------

Tosin Akinosho
