web_server_ip = "192.168.50.101"
db_server_ip = "192.168.50.102"

Vagrant.configure("2") do |config|

  # Configuration for the first virtual machine
  config.vm.define "web_server" do |web_server|
    server_type = "web"
    web_server.vm.box = "ubuntu/bionic64"
    web_server.vm.hostname = "web-server"
    
    web_server.vm.network "private_network", ip: server_type == "web" ? web_server_ip : db_server_ip

    web_server.vm.synced_folder ".", "/vagrant_data"

    web_server.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
      echo "#{db_server_ip}    db-server" >> /etc/hosts
    SHELL

        web_server.vm.provider "virtualbox" do |vb|
          vb.name = "Web Server"
        end
  end

  # Configuration for the second virtual machine
  config.vm.define "db_server" do |db_server|
    server_type = "db"
    db_server.vm.box = "ubuntu/bionic64"
    db_server.vm.hostname = "db-server"
    
    db_server.vm.network "private_network", ip: server_type == "web" ? web_server_ip : db_server_ip

    db_server.vm.synced_folder ".", "/vagrant_data"

    db_server.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y mysql-server
      echo "#{web_server_ip}    web-server" >> /etc/hosts
    SHELL

      db_server.vm.provider "virtualbox" do |vb|
        vb.name = "Database Server"
      end
  end

  # Custom settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = "2"
  end

end