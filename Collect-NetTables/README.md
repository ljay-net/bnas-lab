This folder contains source code for summary report exercise

Playbook collects ARP/MAC address tables from different devices and store them in folder
There are plays for ios, nxos and asa devices and respective parsing and presentation templates.
Playbook assumes that inventory file is grouped according to os and uses *network_cli* connection and respective *ansible_network_os* variables 
- NX-OS requres json output.
- IOS and ASA use textfsm filters