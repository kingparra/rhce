Vagrant.configure("2") do |config|

  config.vm.box = "generic/rhel9"
  config.vm.synced_folder '.', '/vagrant', disabled: true
  config.ssh.insert_key = false

  config.vm.provider :virtualbox do |v|
    v.memory = 512
    v.cpus = 1
    v.linked_clone = true
  end

  # Define three VMs with static private IP addresses.
  boxes = [
    {:name => "controller",  :ip => "192.168.56.2"},
    {:name => "app1",        :ip => "192.168.56.3"},
    {:name => "app2",        :ip => "192.168.56.4"},
    {:name => "app3",        :ip => "192.168.56.5"}
  ]

  # Create each of the VMs with the name and ips in boxes.
  boxes.each do |opts|
    config.vm.define opts[:name] do |config|
      config.vm.hostname = opts[:name]
      config.vm.network :private_network, ip: opts[:ip]
    end
  end

  # # Provision with ansible after all VMs have been created.
  # config.vm.provision "ansible" do |ansible|
  #   ansible.playbook = "provision/main.yml"
  #   ansible.inventory_path = "provision/inventories/main.ini"
  #   ansible.limit = "all"
  # end

end
