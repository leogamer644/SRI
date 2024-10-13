
# 
Vagrant.configure("2") do |config|
 
  config.vm.define "DHCP" do |d|
    d.vm.box = "debian/bookworm64"
    d.vm.network "private_network",
      ip: "192.168.56.10"
    d.vm.network "private_network",
      ip: "192.168.57.10",
      virtualbox__intnet:true
    d.vm.provision "shell", inline: <<-SHELL
    apt update
     apt install isc-dhcp-server -y
     cp -v /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.bak
     cp -v ../../vagrant/DHCP/dhcpd.conf /etc/dhcp/dhcpd.conf
     cp -v ../../vagrant/DHCP/isc-dhcp-server /etc/default/isc-dhcp-server
     systemctl restart isc-dhcp-server.service
    SHELL
  end
  
  config.vm.define "client1" do |c1|
    c1.vm.box = "debian/bookworm64"
    c1.vm.network "private_network",
      :mac => "222222222222" ,
      auto_config:false,
      virtualbox__intnet:true
    c1.vm.provision "shell", inline: <<-SHELL
     dhclient eth1 -r
     dhclient eth1 
    SHELL
  end

  config.vm.define "client2" do |c2|
    c2.vm.box = "debian/bookworm64"
    c2.vm.network "private_network",
      :mac => "222222222255" ,
      auto_config:false,
      virtualbox__intnet:true
    c2.vm.provision "shell", inline: <<-SHELL
      dhclient eth1 -r
      dhclient eth1 
    SHELL
  end
end
