# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "centos/7"

  config.vm.provision "file", source: "private.pem", destination: "/tmp/private.pem"
  config.vm.provision "file", source: "haproxy.cfg", destination: "/tmp/haproxy.cfg"

  config.vm.provision "shell", inline: <<-SHELL
    sudo yum install -y haproxy
    sudo mkdir -p /etc/ssl/private_tmpfs
    sudo mount -t tmpfs -o size=20m tmpfs /etc/ssl/private_tmpfs
    sudo cp /tmp/private.pem /etc/ssl/private_tmpfs/
    sudo chown root:root /etc/ssl/private_tmpfs/private.pem
    sudo chmod 600 /etc/ssl/private_tmpfs/private.pem
    sudo cp /tmp/haproxy.cfg /etc/haproxy/
    sudo systemctl start haproxy
    sleep 5
    sudo systemctl status haproxy
  SHELL

end
