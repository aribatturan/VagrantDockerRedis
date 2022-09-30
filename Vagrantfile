# -*- mode: ruby -*-
# vi: set ft=ruby :


cluster = {
  "master" => { :ip => "192.168.44.10", :cpus => 2, :mem => 4096 }
}

Vagrant.configure("2") do |config|
  config.vm.box = "geerlingguy/ubuntu2004"

  cluster.each_with_index do |(hostname, info), index|
    config.vm.define hostname do |cfg|
      cfg.vm.network :private_network, ip: "#{info[:ip]}"
      cfg.vm.hostname = hostname
      cfg.vm.provider "virtualbox" do |vb|
        # Display the VirtualBox GUI when booting the machine
        vb.gui = false
      
        # Customize the amount of memory on the VM:
        vb.memory = info[:mem]
        vb.cpus = info[:cpus]
      end

      cfg.vm.provision "shell", inline: "/vagrant/docker-installer.sh"
      
    end
  end
end