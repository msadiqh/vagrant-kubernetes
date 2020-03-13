Vagrant.configure("2") do |config|

  config.vm.box = "bento/ubuntu-18.04"

  config.vm.define "master_box" do |master|
      master.vm.hostname = "master.local"
      master.vm.network :private_network, ip: "192.168.3.100"
      master.vm.provider :virtualbox do |v|
         v.gui = false
         v.cpus = 2
         v.memory = 2048
     end
  end
  
  config.vm.define "node1_box" do |node1|
      node1.vm.hostname = "node1.local"
      node1.vm.network :private_network, ip: "192.168.3.101"
      node1.vm.provider :virtualbox do |v|
         v.gui = false
         v.memory = 3000
     end
  end
  
    config.vm.define "node2_box" do |node2|
      node2.vm.hostname = "node2.local"
      node2.vm.network :private_network, ip: "192.168.3.102"
      node2.vm.provider :virtualbox do |v|
         v.gui = false
         v.memory = 3000
     end
  end
    
  config.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/cluster-setup.yml"

      ansible.groups = {
          "master_server" => ["master", "master_box"],
          "node_server" => ["node1", "node2", "node1_box", "node2_box"],
      }
  end
 
   if Vagrant.has_plugin?("vagrant-hostmanager")
      config.hostmanager.enabled = true
      config.hostmanager.manage_host = true
      config.hostmanager.manage_guest = true
  end
end
