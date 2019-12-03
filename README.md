# bnas-lab

This repository contains lab topology and varios files used in lab exersises of [Building Network Automation Solution course](https://my.ipspace.net/bin/list?id=NetAutSol)

### Ansible host setup:
- Primary host to run tasks is VM with ansible and other installed tools
- Same tools are available on local machine and would be run in python virtual enviroment 

### Topology LAB setup:
- Cisco VIRL is platform for building test labs
- VIRL instance is running on ESXi cluster and available at ***virl.eng.company.local***
- VIRL VM has 2 shared flat networks routeble to physical network

### Test topology 
- Basic topology has several devices representing various network os's needed for automation tasks:
  - IOS for routers and L2 switches
  - NX-OS for distribution and core 
  - ASA for firewalls
- VIRL flat network is used as OOB to connect to those devices
- As a first step, for simple tests, topology looks like: `S1-r1 - S1-sw1 - S1-fw1` with flat as OOB 
- Topology can be extended as needed by adding more devices in VIRL or adding physical by interconnecting via flat1
