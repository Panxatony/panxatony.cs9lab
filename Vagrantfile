# -*- mode: ruby -*-
# vi: set ft=ruby :

$script = <<SCRIPT
echo Start updates
sudo /usr/bin/yum update -y
echo END
echo Start RDO INstall
sudo yum install -y https://www.rdoproject.org/repos/rdo-release.rpm
sudo yum install -y openstack-packstack
sudo packstack --allinone
echo I am provisioning...
SCRIPT

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config| 
  config.ssh.insert_key = false
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "2048"] 
  end
  
  # openstack server.
  config.vm.define "openstack" do |openstack|
    openstack.vm.hostname = "packstack.cs9demo.lab"
    openstack.vm.box = "geerlingguy/centos7"
    openstack.vm.network :private_network, ip: "192.168.60.5"

    # Run Ansible provisioner once for all VMs at the end.
    #openstack.vm.provision "ansible" do |ansible| 
    #  ansible.playbook = "configure.yml"
    #  ansible.inventory_path = "inventories/vagrant/inventory"
    #  ansible.limit = "all"
    #  ansible.extra_vars = {
    #    ansible_ssh_user: 'vagrant',
    #    ansible_ssh_private_key_file: "~/.vagrant.d/insecure_private_key"
    #  }
    #end
    openstack.vm.provision "shell", inline: $script
    # Run shell script 

  end
end