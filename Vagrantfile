# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT
echo I am provisioning...
date > /etc/vagrant_provisioned_at

composer self-update
sudo -u vagrant composer global update
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true

  config.vm.box = "black-dev"
  config.vm.box_url = "packer/box/black-virtualbox.box"

  config.vm.hostname = 'black-dev'
  config.vm.network :private_network, ip: "192.168.169.70"

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder "../", "/var/www/black", type: "nfs"

  config.hostmanager.aliases = %w(
    black.dev
  )

  config.vm.provision "shell", inline: $script

  config.vm.provider "virtualbox" do |v|
    v.memory = "1024"
    v.cpus = "1"
    v.name = "black-dev"
  end

end
