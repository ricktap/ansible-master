# decide wether to use ansible from your host (false) or
# to install it onto the vm (true) and run it from there
ansible_local = false

Vagrant.configure("2") do |config|
    # webserver
    config.vm.define "web" do |web|
        web.vm.box = "centos/7"
        web.vm.network "private_network", ip: "10.10.0.102"
        web.vm.hostname = "web"
    end

    # database server
    config.vm.define "db" do |db|
        db.vm.box = "centos/7"
        db.vm.network "private_network", ip: "10.10.0.103"
        db.vm.hostname = "db"
    end

    # a test server, that consists of a webserver and a database
    config.vm.define "test" do |testvm|
        testvm.vm.box = "centos/7"
        testvm.vm.network "private_network", ip: "10.10.0.104"
        testvm.vm.hostname = "test"
    end

    # the ansible master, that provisions the three other servers
    config.vm.define "master", primary: true do |master|
        master.vm.box = "centos/7"
        master.vm.network "private_network", ip: "10.10.0.101"
        master.vm.hostname = "master"

        if ansible_local
        # provision using a local ansible installation on the vm
            master.vm.provision "ansible_local" do |ansible|
                print "running ansible on the master vm... \n"
                ansible.install = true
                ansible.install_mode = "default"
                ansible.playbook = "master_playbook.yml"
                ansible.provisioning_path = "/vagrant/ansible"
            end
        else
        # provision using the hosts own ansible installation
            master.vm.provision "ansible" do |ansible|
                print "running ansible on your host... \n"
                ansible.playbook = "ansible/master_playbook.yml"
            end
        end
    end
end
