# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = "ubuntu/trusty"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.network :private_network, ip: "192.168.33.15"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "5000"]
  end

  # Shared folder from the host machine to the guest machine. Uncomment the line
  # below to enable it.
  config.vm.synced_folder "../vida", "/vida", mount_options: ["dmode=777,fmode=777"]

  config.vm.network "forwarded_port", guest: 80, host: 8888

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "vagrant.yml"
    ansible.host_key_checking = false
    ansible.verbose = "v"
    ansible.inventory_path = "vagrant_server"
    ansible.limit = "vida"
  end
end
