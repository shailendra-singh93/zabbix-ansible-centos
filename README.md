## Overview

Ansible-playbook for
Centos-7 or Centos-8 Environment to install
Zabbix4.0-server(rpm) and
Zabbix-agent(rpm)

## Target Environment

* CentOS7 ( or CentOS8 )
* Prepare centos-VMs and install git and ansible
* Setup ssh

## common setting 

* os(common)
	+ selinux
	+ hostname
	+ timezone(zone Asia/Kolkata)
	+ zabbix-repo

* zabbix-server
  + Firewall setting for services(http,snmptrap,zabbix-server)
  + zabbix4.0(zabbix official repo)
  + httpd, php, db(mariadb or mysql)
  + support for CentOS8: mariadb/mysql (https://support.zabbix.com/browse/ZBX-16465)
	
  
* zabbix-agent
	+ zabbix-agent4.0
  + zabbix-agent settings(Server,ServerActive,HostnameItem)

# Inventory details is specified below

* zabbix-ansible-centos/inventory/inventory.ini

```
[servers] ... zabbix server
[agents] ... zabbix-agent client
[all:vars] ... vars(Variables for all)
[servers:vars] ... vars(For servers)
```

Temporary inventory details set as below（Change it as per your environment)
```
[servers]
test-ui ansible_ssh_host=192.168.133.254 ansible_ssh_user=root
[agents]
haproxy-test ansible_ssh_host=192.168.133.160 ansible_ssh_user=root
[all:vars]
timezone="Asia/Kolkata"
zabbix_server_ip="192.168.133.254"
[servers:vars]
zabbix_mysql_password="password"
```

### Execute Playbooks as below

(Run on ansible server)
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
