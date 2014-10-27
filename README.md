vagrant-squid-deb-proxy
=======================

Simple squid-deb-proxy image for caching deb packages.

## Prerequisites

1. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
1. Install [Vagrant](https://www.vagrantup.com/downloads)


## Installation

1. Clone this repository

        git clone https://github.com/millerjp/vagrant-squid-deb-proxy.git
        cd vagrant-squid-deb-proxy

1. The default static IP is `10.211.99.100`.

1. Start the VM

        vagrant up

1. In the provisioning script for your other VMs, include these steps (adjusting IP address if you've changed it):

        # install and configure for local debian proxy (if present)
        apt-get install squid-deb-proxy-client -y
        echo 'Acquire::http::Proxy "http://10.211.99.100:8000/";' | sudo tee /etc/apt/apt.conf.d/30autoproxy
		

1. Now start your other VMs as normal. They should start using this VM as a proxy/cache during any `apt-get` commands.

## Notes
1. Connect up to the VM

        vagrant ssh

1. Tail the squid logs

        sudo tail -1000f /var/log/squid-deb-proxy/access.log
	


## Credit

This has been copied and and modified for my set-up from [Brian Cantoni's](https://github.com/bcantoni) project: https://github.com/bcantoni/vagrant-deb-proxy . He has some great Vagrant images - check them out.

## Licence

This is distributed under [Apache License v2](https://www.apache.org/licenses/LICENSE-2.0.html) and comes without any support. But feel free to use it :)
