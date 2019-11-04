# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "base"
        config.vm.define "master" do |master|
            master.vm.box = "ubuntu/bionic64"
            master.vm.hostname = "master.example.com"
            master.vm.network "private_network", ip: "172.16.1.100"
        end

        config.vm.define "node1" do |node1|
            node1.vm.box = "ubuntu/bionic64"
            node1.vm.hostname = "node1.example.com"
            node1.vm.network "private_network", ip: "172.16.1.201"
        end

        config.vm.define "node2" do |node2|
            node2.vm.box = "ubuntu/bionic64"
            node2.vm.hostname = "node2.example.com"
            node2.vm.network "private_network", ip: "172.16.1.202"
        end
        
        config.vm.provision "shell", inline: <<-SHELL
        echo 172.16.1.100 master.example.com master >> /etc/hosts
        echo 172.16.1.201 node1.example.com node1 >> /etc/hosts
        echo 172.16.1.202 node2.example.com node2 >> /etc/hosts
        echo root:redhat | sudo chpasswd
        sed -i '/PasswordAuthentication/s/no/yes/' /etc/ssh/sshd_config
        sed -i '/^#PermitRootLogin/s/#//' /etc/ssh/sshd_config
        systemctl restart sshd
        SHELL
    end