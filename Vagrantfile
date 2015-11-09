Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.
  
  config.vm.box = "boxcutter/ubuntu1404" # using the boxcutter box as it works across vmware, parallels and virtualbox.

  config.vm.network "public_network"
  config.vm.network "forwarded_port", guest: 5000, host: 5000


  # Enable provisioning with a shell script.
  config.vm.provision "shell", path: "provision.sh"
end

