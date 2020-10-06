$script_nginx = <<-SCRIPT
  apt-get update && \
  apt-get install nginx
SCRIPT


Vagrant.configure("2") do |config|
  
  config.vm.box = "hashicorp/bionic64"

  config.vm.network "forwarded_port", guest: 80, host: 8181
  #config.vm.network "public_network"
  
  config.vm.provider "virtualbox" do |vbx|
    vbx.memory = 5
    vbx.cpus = 1
  end 

  config.vm.define "config_shell" do |config_shell| 
    config_shell.vm.provision "shell", inline: $script_nginx
  end

  config.vm.define "mysqlserver" do |mysqlserver|
    mysqlserver.vm.network "public_network", ip: "192.168.15.28"
  end

  config.vm.define "ansible" do |ansible|
    ansible.vm.network "public_network", ip: "192.168.15.31"
    ansible.vm.provision "shell", 
      inline: "apt-get update && \
              apt-get install -y software-properties-common && \
              apt-add-repository --yes --update ppa:ansible/ansible && \
              apt-get install -y ansible"
  end
end
