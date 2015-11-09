Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.
  
  config.vm.box = "boxcutter/ubuntu1404" # using the boxcutter box as it works across vmware, parallels and virtualbox.

  config.vm.network "public_network"

  # Enable provisioning with a shell script.
  config.vm.provision "shell", privileged: false, path: "provision.sh"
end

