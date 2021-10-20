$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server-5.7 && \
  cat /vagrant/mysql/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf && \
  service mysql restart
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  config.vm.network "forwarded_port", guest: 3306, host: 3306, host_ip: "127.0.0.1"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 2
  end

  # Minhas configs de chave ssh
  config.ssh.insert_key = false
  config.ssh.private_key_path = ["private_keys", "C:/Users/thales/.vagrant.d/insecure_private_key"]
  config.vm.provision "file", source: "private_keys.pub", destination: "authorized_keys"
  
  config.vm.define "atv1" do |atv1|

    atv1.vm.provider "virtualbox" do |vb|
      vb.name = "atv1"
    end

    atv1.vm.provision "shell", inline: $script_mysql
    
  end
  
end

#remover o apache do script, fazer funcionar no localhost na porta certa, enviar para o git, mandar o link do git para o professor