disk = './secondDisk.vdi'
disk2 = './secondDisk2.vdi'

Vagrant.configure("2") do |config|

  config.vm.define "master" do |master|
    master.vm.box = "centos/7"
    master.vm.hostname = "master-vm-centos"
    master.vm.network "private_network", ip: "192.168.2.10"
    master.vm.synced_folder '.', '/vagrant', type: 'virtualbox'
    master.vm.provider "virtualbox" do |v|
      unless File.exist?(disk)
        v.customize ['createhd', '--filename', disk, '--variant', 'Fixed', '--size', 20 * 1024]
      end
      v.customize ['storageattach', :id,  '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk]
      v.memory = 1024
      v.cpus = 2
    end
    master.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.limit = 'all'
      ansible.inventory_path = 'hosts'
      ansible.become = true
      #ansible.galaxy_role_file = "requirements.yml"
      #ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path}"
    end
  end

  config.vm.define "worker" do |worker|
    worker.vm.box = "centos/7"
    worker.vm.hostname = "worker-vm-centos"
    worker.vm.network "private_network", ip: "192.168.2.11"
    worker.vm.synced_folder '.', '/vagrant', type: 'virtualbox'
    worker.vm.provider "virtualbox" do |v|
      unless File.exist?(disk2)
        v.customize ['createhd', '--filename', disk2, '--variant', 'Fixed', '--size', 20 * 1024]
      end
      v.customize ['storageattach', :id,  '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', disk2]
      v.memory = 1024
      v.cpus = 2
    end
    worker.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.limit = 'all'
      ansible.inventory_path = 'hosts'
      ansible.become = true
      #ansible.galaxy_role_file = "requirements.yml"
      #ansible.galaxy_command = "sudo ansible-galaxy install --role-file=%{role_file} --roles-path=%{roles_path}"
    end
  end    

end