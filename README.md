Ansible Role: IPA Client
========================

Install IPA Client Service and configure/reconfigure the client.


Requirements
------------
Requires an reachable IPA Server to configure. Default we are using the FreeIPA server provided by Redhat [here](http://www.freeipa.org/page/Demo)


Role Variables
--------------
Mandatory variable are listed here with default values :

	ipaserver_realm: "DEMO1.FREEIPA.ORG"
	ipaserver_domain: "demo1.freeipa.org"

	ipaserver_admin_username : * * * * * * * * * * * 
	ipaserver_admin_password : * * * * * * * * * * * 


Optional variables are listed here with default values :

	ipaclient_reconfigure : False 

	ipaclient_configure_ssh: True
	ipaclient_configure_sshd: True
	ipaclient_mkhomedir: True
	ipaclient_ssh_trust_dns: False
	ipaclient_setup_ntp: False  #ansible-role-common will set NTP


Dependencies
------------

	- [yabhinav.common](https://galaxy.ansible.com/yabhinav/common/)


Example Playbook
----------------

```yaml
- hosts: localhost
  become_user: True
  gather_facts: True
  
  roles:
    - yabhinav.ipaserver
```

Issues
------

- It is not advised to execute this role from ansible running on python-virtualenv on Ubuntu16.04 locally due to this [issue](https://github.com/pypa/virtualenv/issues/1022) . Also have a look at same [issue here](https://github.com/ansible/ansible/issues/21691) and [here](https://bugs.launchpad.net/ubuntu/+source/freeipa) for other ipaclient-installer script issues
- Freeipa-admintools is available only in Ubuntu16.04, So Debian 7,8 and Ubuntu 12.04 and 14.04 support not present for this role
- [rpcbind installation hangs ](https://github.com/yabhinav/docker-ansible-images/issues/4) when installing ipa-client on `CentOS7` image rpcbind installation  hangs the both ansibe playbook and docker exec  commands alike, hence add it to image directly as a necessary package.


License
-------

MIT


Author Information
------------------

Created by [Abhinav Yalamanchili](https://yabhinav.github.com)
