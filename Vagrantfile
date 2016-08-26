Vagrant.configure(2) do |config|
  config.vm.box = "bento/ubuntu-16.04"
  config.vm.box_check_update = false
  config.vm.network "public_network", type: "dhcp"
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook/main.yml"
    ansible.verbose = "v"
  end
end
