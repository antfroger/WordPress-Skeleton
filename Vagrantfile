Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provision "shell" do |s|
    s.path = "provision/setup.sh"
    # come from local-config.php
    s.args = ["wp", "root", "root"]
  end
end