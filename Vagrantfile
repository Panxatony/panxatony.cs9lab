# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config| 
  config.ssh.insert_key = false
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"] 
  end
  
  # ELK Server.
  config.vm.define "mgmt" do |mgmt|
    mgmt.vm.hostname = "mgmtsrv.cs9demo.local"
    mgmt.vm.box = "geerlingguy/centos7"
    mgmt.vm.network :private_network, ip: "192.168.60.4"
  end

  # ELK Server.
  config.vm.define "elk" do |elk|
    elk.vm.hostname = "elksrv.cs9demo.local"
    elk.vm.box = "geerlingguy/centos7"
    elk.vm.network :private_network, ip: "192.168.60.7"
  end

  # OMD server.
  config.vm.define "omd" do |omd|
    omd.vm.hostname = "omdsrv.cs9demo.local"
    omd.vm.box = "geerlingguy/centos7"
    omd.vm.network :private_network, ip: "192.168.60.6"
  end

  # Gitlab server.
  config.vm.define "gitlab" do |gitlab|
    gitlab.vm.hostname = "gitlab.cs9demo.local"
    gitlab.vm.box = "geerlingguy/centos7"
    gitlab.vm.network :private_network, ip: "192.168.60.8"
  end

  # FreeIPA server.
  config.vm.define "freeipa" do |freeipa|
    freeipa.vm.hostname = "ipasrv.cs9demo.local"
    freeipa.vm.box = "geerlingguy/centos7"
    freeipa.vm.network :private_network, ip: "192.168.60.5"

    config.vm.provision "ansible" do |ansible|
    ansible.playbook = "bootstrap-lab.yml"
      ansible.inventory_path = "inventories/vagrant/inventory"
      ansible.limit = "all"
      ansible.extra_vars = {
        ansible_ssh_user: 'vagrant',
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
    end
  end
end