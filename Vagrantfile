Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.
  
  #config.vm.box = "ubuntu/trusty64" # use this for virtualbox based setups
  config.vm.box = "parallels/ubuntu-14.04" # use this when using parallels on a mac.
  config.vm.network "public_network"
  #config.vm.network "forwarded_port", guest: 5000, host: 5000


  # Enable provisioning with a shell script.
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
    echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
    sudo apt-get update
    sudo apt-get install -y mono-complete
    
    sudo apt-get install -y unzip automake libtool curl
    
    curl -sSL https://github.com/libuv/libuv/archive/v1.4.2.tar.gz | sudo tar zxfv - -C /usr/local/src
    cd /usr/local/src/libuv-1.4.2
    sudo sh autogen.sh
    sudo ./configure
    sudo make 
    sudo make install
    sudo rm -rf /usr/local/src/libuv-1.4.2 && cd ~/
    sudo ldconfig
    
    curl -sSL https://raw.githubusercontent.com/aspnet/Home/dev/dnvminstall.sh | DNX_BRANCH=dev sh && source ~/.dnx/dnvm/dnvm.sh
    dnvm upgrade
    sudo apt-get install -y curl
    curl -sL https://deb.nodesource.com/setup | sudo bash -
    sudo apt-get update
    sudo apt-get -y install nodejs
    sudo apt-get install build-essential libssl-dev
    sudo npm update -g npm  
    sudo npm install -g yo  
    sudo npm install -g generator-aspnet  
  SHELL
end

