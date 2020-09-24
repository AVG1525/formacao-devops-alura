$script_nginx = <<-SCRIPT
  apt-get update && \
  apt-get install nginx
SCRIPT

$script_ansible = <<-SCRIPT
  apt-get update && \
  apt-get -y install software-properties-common && \
  apt-add-repository --yes --update ppa:ansible/ansible && \
  apt-get install -y ansible
SCRIPT

Vagrant.configure("2") do |config|
  
  config.vm.box = "hashicorp/bionic64"

  #config.vm.network "public_network", guest: 80, host: 8181
  #config.vm.network "public_network"
    

  config.vm.define "config_shell" do |config_shell| 
    config_shell.vm.provision "shell", inline: $script_nginx
  end

  config.vm.define "mysqlserver" do |mysqlserver|
    mysqlserver.vm.network "forwarded_port", ip: "192.168.15.21"
  end

  config.vm.define "ansible" do |ansible|
    ansible.vm.network "forwarded_port", ip: "192.168.15.20"
    ansible.vm.provision "shell", inline: $script_ansible
  end
end
