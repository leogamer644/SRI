Vagrant.configure("2") do |config|
  config.vm.box = "debian/bullseye64"
    config.vm.define "revproxy" do |revproxy|
    revproxy.vm.network "private_network", ip: "192.168.57.10"
    revproxy.vm.network "forwarded_port", guest: 80, host: 8080
    revproxy.vm.provision "shell", inline: <<-SHELL
    apt-get update
     apt-get install -y ngnix
    SHELL
  end
  config.vm.box = "rockylinux/9"
    config.vm.define "database" do |database|
    database.vm.network "private_network", ip:"192.168.57.11"
    database.vm.provision "shell", inline: <<-SHELL
    dnf install mariadb-server
    systemctl enable mariadb
    SHELL
    end
  config.vm.box = "ubuntu/focal64"
    config.vm.define "app" do |app|
    app.vm.network "private_network", ip:"192.168.57.13"
    app.vm.provision "shell", inline: <<-SHELL
    apt update
     apt install python3-venv python3-pip
     mkdir -p flaskapp/templates
     cd flaskapp
     python3 -m venv virtualenv
     source virtualenv/bin/activate
     pip3 install flask gunicorn
    SHELL
    end

end
