Vagrant.configure("2") do |config|

  # Configuration for the first virtual machine
  config.vm.define "web_server" do |web_server|
    web_server.vm.box = "ubuntu/bionic64"
    web_server.vm.hostname = "web-server"
    
    # Network settings
    web_server.vm.network "private_network", ip: "192.168.50.101"

    # Synced folder
    web_server.vm.synced_folder ".", "/vagrant_data"

    # Provisioning
    web_server.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
    SHELL
        # VirtualBox-specific settings
        web_server.vm.provider "virtualbox" do |vb|
          vb.name = "Web Server"
        end
  end

  # Configuration for the second virtual machine
  config.vm.define "db_server" do |db_server|
    db_server.vm.box = "ubuntu/bionic64"
    db_server.vm.hostname = "db-server"
    
    # Network settings
    db_server.vm.network "private_network", ip: "192.168.50.102"

    # Synced folder
    db_server.vm.synced_folder ".", "/vagrant_data"

    # Provisioning
    db_server.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y mysql-server
    SHELL

      # VirtualBox-specific settings
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