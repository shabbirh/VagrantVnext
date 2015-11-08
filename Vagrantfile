Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.
  
  config.vm.box = "boxcutter/ubuntu1404" # using the boxcutter box as it works across vmware, parallels and virtualbox.

  config.vm.network "public_network"
  #config.vm.network "forwarded_port", guest: 5000, host: 5000


  # Enable provisioning with a shell script.
  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    echo "Making sure OS is properly updated"
    sudo apt-get update
    sudo apt-get -y upgrade
    echo "Installing Mono"
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
    echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
    sudo apt-get update
    echo "Installing mono and other required libraries/tools"
    sudo apt-get install -y mono-complete
    sudo apt-get install -y unzip automake libtool curl git-core zsh
    curl -sSL https://github.com/libuv/libuv/archive/v1.4.2.tar.gz | sudo tar zxfv - -C /usr/local/src
    cd /usr/local/src/libuv-1.4.2
    sudo sh autogen.sh
    sudo ./configure
    sudo make 
    sudo make install
    sudo rm -rf /usr/local/src/libuv-1.4.2 && cd ~/
    sudo ldconfig
    echo "Installing DNVM and grabbing most current DNVM layer"
    curl -sSL https://raw.githubusercontent.com/aspnet/Home/dev/dnvminstall.sh | DNX_BRANCH=dev sh && source ~/.dnx/dnvm/dnvm.sh
    dnvm upgrade
    echo "Installing Nodejs"
    sudo apt-get install -y curl
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get update
    sudo apt-get -y install nodejs
    sudo apt-get -y install build-essential libssl-dev
    echo "Upgrading Npm and installing the Yoman Generator"
    sudo npm update -g npm  
    sudo npm install -g yo  
    sudo npm install -g generator-aspnet  
    echo "Organising Zsh and your working environment"
    git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
    cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
    sudo chsh -s /bin/zsh vagrant
    curl https://raw.githubusercontent.com/shabbirh/VagrantVnext/master/zshrc.default > ~/.zshrc
    sudo apt-get -y install software-properties-common python-software-properties
    sudo add-apt-repository ppa:djcj/screenfetch
    sudo apt-get update
    sudo apt-get -y install fortune
    sudo apt-get -y install screenfetch
    sudo apt-get -y install htop
    echo "Ready to go - enjoy!"
    echo "=== IMPORTANT NOTE ==="
    echo "Be sure to add --server.urls http://0.0.0.0:5000 to the"
    echo "'web' definition in your project.json file if you want to see anything on your host :)"
    echo ""
  SHELL
end

