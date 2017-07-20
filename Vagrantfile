Vagrant.configure("2") do |config|
    config.vm.define "web" do |web|
        web.vm.box = "centos/7"
        web.vm.network "private_network", ip: "10.10.0.102"
        web.vm.hostname = "web"
    end

    config.vm.define "db" do |db|
        db.vm.box = "centos/7"
        db.vm.network "private_network", ip: "10.10.0.103"
        db.vm.hostname = "db"
    end

    config.vm.define "test" do |testvm|
        testvm.vm.box = "centos/7"
        testvm.vm.network "private_network", ip: "10.10.0.104"
        testvm.vm.hostname = "test"
    end

    config.vm.define "master", primary: true do |master|
        master.vm.box = "centos/7"
        master.vm.network "private_network", ip: "10.10.0.101"
        master.vm.hostname = "master"

        master.vm.provision "file", source: "./.vagrant/machines/web/virtualbox/private_key", destination: "/home/vagrant/.ssh/id_web"
        master.vm.provision "file", source: "./.vagrant/machines/db/virtualbox/private_key", destination: "/home/vagrant/.ssh/id_db"
        master.vm.provision "file", source: "./.vagrant/machines/test/virtualbox/private_key", destination: "/home/vagrant/.ssh/id_test"
        master.vm.provision "file", source: "./ssh_config", destination: "/home/vagrant/.ssh/config"
        master.vm.provision "shell", inline: "chmod 600 /home/vagrant/.ssh/id_*"
        master.vm.provision "shell", inline: "chmod 600 /home/vagrant/.ssh/config"
    end
end
