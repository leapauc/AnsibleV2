#  -*-  mode:  ruby -*-
# vi: set ft=ruby  :

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION)  do  |config|
  # General Vagrant VM   configuration.
  config.vm.box  =  "ubuntu/jammy64"
  config.ssh.insert_key  =  false
  config.vm.synced_folder  ".",  "/vagrant",  disabled:  true
  config.vm.provider  :virtualbox  do  |v|
  	v.memory  =  1024
  	v.linked_clone  =  true
	end

  #  ControlMaster
  config.vm.define  "master"  do  |app|
    app.vm.hostname  =  "master.dev"
    app.vm.network  :private_network,  ip:  "192.168.56.1"
  end

	#  Application  server 1.
	config.vm.define  "VM1"  do  |app|
  	app.vm.hostname  =  "VM1.web"
  	app.vm.network  :private_network,  ip:  "192.168.56.2"
	end

	#  Database  server.
	config.vm.define  "VM2"  do  |db|
  	db.vm.hostname  =  "VM2.db"
  	db.vm.network  :private_network,  ip:  "192.168.56.3"
	end
end

