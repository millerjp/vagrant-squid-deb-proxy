# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrant squid-deb-proxy VM
# Sets up a simple VM with a Squid proxy/cache to speed up local package installs for Debian/Ubuntu
# Credit to Brian Cantoni https://github.com/bcantoni/vagrant-deb-proxy - updated for my set-up.


# Adjustable settings
CFG_MEMSIZE = "512"      # max memory for each VM
CFG_IP = "10.211.99.100"  # private IP address

node_script = <<SCRIPT
#!/bin/bash

# install a few base packages
apt-get update
apt-get install vim curl python-pip squid-deb-proxy squid-deb-proxy-client -y

SCRIPT


# VM configurations
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :debcache do |x|
    x.vm.box = "hashicorp/precise64"
    x.vm.provider "vmware_fusion" do |v|
      v.vmx["memsize"]  = CFG_MEMSIZE
    end
    x.vm.provider :virtualbox do |v|
      v.name = "squid-deb-proxy"
      v.customize ["modifyvm", :id, "--memory", CFG_MEMSIZE]
    end
    x.vm.network :private_network, ip: CFG_IP
    x.vm.hostname = "squid-deb-proxy"
    x.vm.provision :shell, :inline => node_script
  end
end
