$script_nginx = <<-SCRIPT
  echo sudo apt update && sudo apt install nginx
SCRIPT

Vagrant.configure("2") do |config|
  
  config.vm.box = "hashicorp/bionic64"
  
  config.vm.network "forwarded_port", guest: 80, host: 8181
  config.vm.network "public_network"
  
  config.vm.provision "shell", inline: $script_nginx
end
