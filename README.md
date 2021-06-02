quarkuscoffeeshop-majestic-monolith tower role
=========

quarkuscoffeeshop-majestic-monolith is an application that can be deployed using RHEL edge.  This repo uses the applications found in [RHEL Edge Application collection](https://github.com/tosin2013/rhel-edge-application-collection). This tole will be used in ansible tower to deploy to instances. Check out  the [quarkuscoffeeshop-majestic-monolith project](https://github.com/jeremyrdavis/quarkuscoffeeshop-majestic-monolith) for the source code.

Requirements
------------
* ansible.posix.sysctl
```
ansible-galaxy collection install ansible.posix
ansible-galaxy collection install containers.podman
ansible-galaxy collection install community.general.lvol
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

ScreenShots
------------------------------------------------
![CofffeShop](images/coffeeshop.png)

Role Variables
--------------
Type  | Description  | Default Value
--|---|--
external_endpoint | The External UR of your rhel edge device | 192.168.1.10
rhsm_user | Red Hat user for subscription and registry login  |  user
rhsm_password | Red Hat password for subscription and registry login  |  password
rhsm_unregister | Un register device |  false
network_name | Internal Podman network name |  rhel-edge
podman_ip_range | ip range of podman network |  192.168.22.128/25
podman_subnet | ip subnet of podman network |  192.168.22.0/24
podman_gateway | gateway of podman network |  192.168.22.1
expose_port | quarkuscoffeeshop-majestic-monolith port |  8080
store_id | store id |  ATLANTA # accepted values [RALEIGH, ATLANTA, CHARLOTTE]
container_image | quarkuscoffeeshop-majestic-monolith repo |  "jeremydavis/quarkuscoffeeshop-majestic-monolith-jvm"
container_tag | quarkuscoffeeshop-majestic-monolith version | "1.0.2"
startup_wait_time | startup wait time for  quarkuscoffeeshop-majestic-monolith |  30
pgsql_url | postgresql url|  "jdbc:postgresql://{{ external_endpoint }}:5432/coffeeshopdb?currentSchema=coffeeshop"
pgsql_user | postgresql user |  coffeeshopuser
pgsql_password | postgresql password |  "redhat-21"
pgsql_url_barista | postgresql barista url  |  "jdbc:postgresql://{{ external_endpoint }}:5432/coffeeshopdb?currentSchema=barista"
pgsql_user_barista | postgresql barista user |  "coffeeshopuser"
psql_password_barista | postgresql barista password |  "redhat-21"
pgsql_url_kitchen | postgresql kitchen url |  "jdbc:postgresql://{{ external_endpoint }}:5432/coffeeshopdb?currentSchema=kitchen"
pgsql_user_kitchen | postgresql kitchen user   |  "coffeeshopuser"
pgsql_password_kitchen | postgresql kitchen password   |  "redhat-21"
pg_direcoty_path | default postgres database path | "/pgadmin4"
pg_database_name | default database name for application |  coffeeshopdb
pg_database_password | default database password| redhat-21
pg_database_user | default postgres username | coffeeshopuser
pg_postgres_port | default postgres port | 5432
pg_container_image | postgres container image location | registry.redhat.io/rhel8/postgresql-12
pgadmin_default_email |  pgadmin default email |  user@domain.com
pgadmin_default_password | pgadmin default password |  password
pgadmin_listen_port | pgadmin default port|  5433
pgadmin_container_image | pgadmin default container image |  dpage/pgadmin4:latest
pg_startup_wait_time | pgadmin default container wait startup time |  60
gf_install_plugin | Default plugin URL | "https://github.com/performancecopilot/grafana-pcp/releases/download/v3.0.3/performancecopilot-pcp-app-3.0.3.zip;performancecopilot-pcp-app" 
grafana_port | Default Grafana Port | 3000
gf_container_image | Grafana image location | registry.redhat.io/rhel8/grafana
gf_container_tag | Grafana image tag | latest


Dependencies
------------
* Ansible

Example Playbook
----------------

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


How-To 
--------

To Deploy 

```
ansible-playbook -i inventory myplaybook.yml  -t deploy
```

To clean up 
```
 ansible-playbook -i inventory myplaybook.yml  -t remove_application
```

To register system (WIP)
```
ansible-playbook -i inventory myplaybook.yml  -t register
```

To deploy Postgres ad pgadmin and quarkuscoffeeshop-majestic-monolith  app 
```
ansible-playbook -i inventory myplaybook.yml  -t deploy_application
```

To deploy Postgres ad pgadmin 
```
ansible-playbook -i inventory myplaybook.yml  -t deploy_postgres
```

To deploy quarkuscoffeeshop-majestic-monolith  app 
```
ansible-playbook -i inventory myplaybook.yml  -t deploy_quarkuscoffeeshop-majestic-monolith
```

Demo Deployments
----------------
* On Ansible


License
-------

BSD

Author Information
------------------

Tosin Akinosho
