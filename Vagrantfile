Vagrant.configure("2") do |config|

  config.vm.define "master" do |master|
    master.vm.box = "centos/7"
    master.vm.hostname = "master-vm-centos"
    master.vm.network "private_network", ip: "192.168.2.10"
    master.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 2
    end
    master.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end

  config.vm.define "worker" do |worker|
    worker.vm.box = "centos/7"
    worker.vm.hostname = "worker-vm-centos"
    worker.vm.network "private_network", ip: "192.168.2.11"
    worker.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.cpus = 2
    end
    worker.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end
end