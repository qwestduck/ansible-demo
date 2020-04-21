# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
    config.ssh.private_key_path = ['~/.vagrant.d/insecure_private_key', '~/.ssh/id_rsa']
    config.vm.provision "file", source: "~/.ssh/id_rsa.pub", destination: "~/.ssh/authorized_keys"
    config.vm.provision "shell", inline: <<-EOC
        sudo sed -i -e "\\#PasswordAuthentication yes# s#PasswordAuthentication yes#PasswordAuthentication no#g" /etc/ssh/sshd_config
        sudo systemctl restart sshd.service
        echo "finished"
    EOC

    config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", "256"]
    end

    config.vm.define "vm01" do |cat|
        cat.vm.hostname = "vm01.fun.lan"
        cat.vm.box = "debian/buster64"
        cat.vm.network :private_network, ip: "192.168.42.101"
    end

    config.vm.define "vm02" do |cat|
        cat.vm.hostname = "vm02.fun.lan"
        cat.vm.box = "debian/buster64"
        cat.vm.network :private_network, ip: "192.168.42.102"
    end
end
