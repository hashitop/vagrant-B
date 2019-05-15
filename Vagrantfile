$web_provision_script = <<-WEB_SCRIPT

apt-get update
apt-get install -y nginx

WEB_SCRIPT

$db_provision_script = <<-DB_SCRIPT

export DEBIAN_FRONTEND="noninteractive"
 
#Input root password of MySQL server for silent mode installation
debconf-set-selections <<< "mysql-server mysql-server/root_password password root"
debconf-set-selections <<< "mysql-server mysql-server/root_password_again password root"
 
#Install MySQL server
apt install -y mysql-server

DB_SCRIPT

Vagrant.configure("2") do |config|

  (1..2).each do |i|
    config.vm.define vm_name="web#{i}" do |node|
      node.vm.box = "hashitop/bananas3"
      node.vm.hostname = vm_name
      node.vm.box_version = "0.0.1"
      node.vm.provision "shell", inline: $web_provision_script
    end
  end

  
  config.vm.box = "hashitop/bananas3"
  config.vm.box_version = "0.0.1"
  config.vm.hostname = "mysql"
  config.vm.provision "shell", inline: $db_provision_script

end
