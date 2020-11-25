## Overview Guide

Ansible-playbook for
CentOS-7 or CentOS-8 Environment to install
Zabbix4.0-server(rpm) on Server-host and
Zabbix-agent(rpm) on Agent-host

## Environment for this setup

* CentOS-7 or CentOS-8
* Prepare CentOS-VMs and install git and ansible using (# sudo yum install -y git ansible)
* Configure ssh-key beteween Server-host and Agent-host as (# ssh-keygen -t rsa, # ssh-copy-id user@<server host IP & agent host IP>)

## Common Setting on both Server-host and Agent-host 

* OS specific common settings
	+ selinux
	+ hostname
	+ timezone(zone Asia/Kolkata)
	+ zabbix-repo

* Zabbix-Server specific seetings
  + Firewall setting for services(http,snmptrap,zabbix-server)
  + zabbix4.0(Zabbix from official repo)
  + httpd, php, db(mariadb or mysql)
  + Support for CentOS-8: mariadb/mysql
	
  
* Zabbix-agent specific settings
	+ zabbix-agent4.0
  + zabbix-agent settings(Server,ServerActive,HostnameItem)

# Inventory details is specified below

* zabbix-ansible-centos/inventory/inventory.ini

```
[servers] ... zabbix-server
[agents] ... zabbix-agent client
[all:vars] ... vars(Variables for all)
[servers:vars] ... vars(For servers)
```

Temporary inventory details set as below（Change it as per your environment)
```
[servers]
zabbix-server ansible_ssh_host=192.168.133.200 ansible_ssh_user=root
[agents]
zabbix-agent ansible_ssh_host=192.168.133.201 ansible_ssh_user=root
[all:vars]
timezone="Asia/Kolkata"
zabbix_server_ip="192.168.133.200"
[servers:vars]
zabbix_mysql_password="password"
```

### Execute Playbooks as below

(Run on Ansible-server/Zabbix-server)
```
Clone repo using cmd as: git clone https://github.com/shailendra-singh93/zabbix-ansible-centos.git
Run the playbook as: ansible-playbook -i inventory/inventory.ini site.yml
```

When Playbook execution is completed successfully, You can access zabbix-server GUI as below:
```
http://{zabbix-server-ip}/zabbix
  ID = Admin
  PASS = zabbix
```
