# Zabbix Auto maintainance update Script
As we manage our Windows Servers in Microsoft Active Directory groups in order to decide when to install updates and/or reboot them, a need to automatically put the in and out of Maintenance periods.


Therefore I have wrote the following script in order to perform exactly this task.
1) Search in ldap for hostgroups prefixed with the variable `${ldap_hostgroup_prefix}`
2) checking if the Hostgroup exists within Zabbix and create it if its missing
3) list all LDAP members of each group and put them in the coresponding zabbix hostgroup
4) removing old/wrong hosts from zabbix hostgroup
5) remove empty zabbix hostgroups
6) Create Maintenance periods with extracted information of group name
The Terminology used to extract the information is as follows: DO_0000_0200 means Thursday 00:00 AM till 02:00 AM (currently the weekdays are named in german, DO for Donnerstag)

Thats about it

## Requirements

 - ldapsearch  
 - jq  
 - curl  
 - awk
 - bash

## Instalation
Place the `zbx_script.conf` in the zabbix configuration file direcotry `/etc/zabbix/`.  
Alternatively you can place the file in your users homedirectory under `~/.zbx_script.conf` or you can call the path to the script file as an optional argument `-c`

Just execute the script file via cron as often as you might think changes will occur in your environment.

