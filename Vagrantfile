# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config| 
  config.ssh.insert_key = false
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"] 
  end
  
  # FreeIPA Server.
  config.vm.define "freeipa" do |freeipa|
    freeipa.vm.hostname = "ipasrv.cs9demo.lab"
    freeipa.vm.box = "geerlingguy/centos7"
    freeipa.vm.network :private_network, ip: "192.168.60.4"
  end

  # OMD server.
  config.vm.define "omd" do |omd|
    omd.vm.hostname = "omd.cs9demo.lab"
    omd.vm.box = "geerlingguy/centos7"
    omd.vm.network :private_network, ip: "192.168.60.5"
  end
  
  # ELK server.
  config.vm.define "elk" do |elk|
    elk.vm.hostname = "elk.cs9demo.lab"
    elk.vm.box = "geerlingguy/centos7"
    elk.vm.network :private_network, ip: "192.168.60.6"

    # Run Ansible provisioner once for all VMs at the end.
    elk.vm.provision "ansible" do |ansible| 
      ansible.playbook = "configure.yml"
      ansible.inventory_path = "inventories/vagrant/inventory"
      ansible.limit = "all"
      ansible.extra_vars = {
        ansible_ssh_user: 'vagrant',
        ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
      }
    end
  end
end