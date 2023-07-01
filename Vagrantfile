# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  #config.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"
  #config.ssh.timeout = 120
  #config.vm.box = "ubuntu/focal64"
  
  config.vm.define "ansible" do |ansible|
	ansible.vm.box = "ubuntu/focal64"
  	ansible.vm.network "private_network", ip: "192.168.56.15"
  	ansible.vm.synced_folder ".", "/vagrant_data"
 
  end

  config.vm.define "postgre" do |postgre|
	postgre.vm.box = "ubuntu/focal64"
  	postgre.vm.network "private_network", ip: "192.168.56.11"
  	postgre.vm.synced_folder ".", "/vagrant_data"
 
  end
  
  config.vm.define "odoo1" do |odoo1|
	odoo1.vm.box = "ubuntu/focal64"
  	odoo1.vm.network "private_network", ip: "192.168.56.10"
  	odoo1.vm.synced_folder ".", "/vagrant_data"
  	
  end
  
  config.vm.define "nginx1" do |nginx1|
	nginx1.vm.box = "ubuntu/focal64"
  	nginx1.vm.network "private_network", ip: "192.168.56.12"
	nginx1.vm.network "forwarded_port", guest: 80, host: 80
  	nginx1.vm.synced_folder ".", "/vagrant_data"
  	
  end
  
  config.vm.define "odoo2" do |odoo2|
	odoo2.vm.box = "generic/debian10"
  	odoo2.vm.network "private_network", ip: "192.168.56.13"
  	odoo2.vm.synced_folder ".", "/vagrant_data"
  	
  end

  config.vm.define "nfs" do |nfs|
	nfs.vm.box = "generic/debian10"
  	nfs.vm.network "private_network", ip: "192.168.56.14"
  	nfs.vm.synced_folder ".", "/vagrant_data"
  	
  end

end
