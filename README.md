# Automated Provisioning customer service

This folder contains playbook to provision infrustructure services for customer deployment. Services includes vlan/svi on switches and vm related objects and nat/acl rules on firewall.
Each customer might have one or multiple datacenters and multiple vm objects in each.

## Automating the following tasks

* Nexus: creation of customer Vlan
* Nexus: creation of SVI's with HSRP configuration
* Nexus: update of ACL if multiple datacenters
* ASA: creation of objects for every vm
* ASA: creation of NAT and security rules

## Roadmap

* Automate VMware: distrubuted_port_groups, folders, etc.
* Automate IPAM provisioning

## How to run this

* Fill customer.yml according to the template
* Generate group variables by running this: ```ansible-playbook generate-group-vars.yml```
* Run main playbook against inventory file: ```ansible-playbook -i <inventory>  main.yml```

## Define Ansible Inventory file like this

```yaml
all:
# these defaults can be overridden for any group in the [group:vars] section
    vars:
        ansible_connection: network_cli
        connection: network_cli
        ansible_ssh_user: admin
        ansible_ssh_pass: !vault
    children:
        dc1:
            children:
                dc1-nxos:
                    hosts:
                        dc1-core1:
                            ansible_host: 10.10.10.2
                            SVI: 2
                        dc1-core2:
                            ansible_host: 10.10.10.3
                            SVI: 3
                dc1-asa:
                    hosts:
                        dc1-efw1:
                            ansible_host: 10.10.11.1
        dc2:
            children:
                dc2-nxos:
                    hosts:
                        dc2-core1:
                            ansible_host: 10.20.10.2
                            SVI: 2
                        dc2-core2:
                            ansible_host: 10.20.10.3
                            SVI: 3
                dc2-asa:
                    hosts:
                        dc1-efw1:
                            ansible_host: 10.20.11.1
        nxos:
            children:
                dc1-nxos:
                dc2-nxos:
            vars:
                ansible_network_os: nxos
        asa:
            children:
                dc1-asa:
                dc2-asa:
            vars:
                ansible_network_os: asa
```
