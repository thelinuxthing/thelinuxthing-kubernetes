# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box = "base"
        config.vm.define "manager" do |manager|
            manager.vm.box = "centos/7"
            manager.vm.hostname = "manager.example.com"
            manager.vm.network "private_network", ip: "172.16.1.100"
        end

        config.vm.define "worker1" do |worker1|
            worker1.vm.box = "centos/7"
            worker1.vm.hostname = "worker1.example.com"
            worker1.vm.network "private_network", ip: "172.16.1.201"
        end

        config.vm.define "worker2" do |worker2|
            worker2.vm.box = "centos/7"
            worker2.vm.hostname = "worker2.example.com"
            worker2.vm.network "private_network", ip: "172.16.1.202"
        end
        
        config.vm.provision "shell", inline: <<-SHELL
        echo 172.16.1.100 manager.example.com manager >> /etc/hosts
        echo 172.16.1.201 worker1.example.com worker1 >> /etc/hosts
        echo 172.16.1.202 worker2.example.com worker2 >> /etc/hosts
        echo root:redhat | chpasswd
        sed -i '/PasswordAuthentication/s/no/yes/' /etc/ssh/sshd_config
        sed -i '/PermitRootLogin/s/prohibit-password/yes/' /etc/ssh/sshd_config
        systemctl restart sshd
        SHELL
    end