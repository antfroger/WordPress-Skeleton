Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.33.10"

  config.vm.provision "file",
    source: "provision/vhosts/dev.my-project.com.conf",
    destination: "/home/vagrant/dev.my-project.com.conf"

  config.vm.provision "shell" do |s|
    s.path = "provision/setup.sh"
    # come from local-config.php
    s.args = ["wp", "root", "root", "dev.my-project.com"]
  end
end