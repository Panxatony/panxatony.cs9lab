Lab Environment used by CS9 installations 
=========

Vagrant and Ansible Playbooks used to install Lab Environment. Actual relase includes

* mgmtsrv.cs9demo.local: VM used as Management Station and FreeIPA admin client
* elksrv.cs9demo.local: VM used as Central Log Server with ElasticSearch, Kibana and Logstash
* omdsrv.cs9demo.local: VM used as System Monitoring Server with OMD (check_mk)
* gitlab.cs9demo.local: VM used as DevOps System with GitLab
* ipasrv.cs9demo.local: VM used as Central Directory & Authentication Server with FreeIPA

t.b.d.

Requirements
------------

* Vagrant (https://www.vagrantup.com)
* VirtualBox (https://www.virtualbox.org)
* Ansible (http://www.ansible.com)

t.b.d.

Variables
--------------

Check ```inventories/vagrant/group_vars``` files

t.b.d.

Dependencies
------------

Used Ansible Roles listed in ```requirements.yml```

t.b.d.

Usage
----------------

Installation and usage:

- Clone Git repository ```git clone https://github.com/Panxatony/panxatony.cs9lab.git```
- Modify ```ansible.cfg```
- Modify ```Vagrantfile``` (optional)
- Install Ansible roles ```ànsible-galaxy install -r requirements.yml```
- Start Vagrant installation with ```vagrant up```
- Add vagrant ssh public key to FreeIPA admin user
- Create FreeIPA sudo Role for admin with !authenticate option
- Execute Configuration Playbook with ```ànsible-playbook -u vagrant configure-lab.yml```

t.b.d.

License
-------

BSD

Author Information
------------------

Panxatony (http://macnemo.tv)
