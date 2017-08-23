# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/xenial64"
  config.ssh.forward_agent = true


  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "https://app.vagrantup.com/ubuntu/boxes/xenial64"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.network "private_network", ip: "192.168.100.101"


  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
  ###config.vm.provision "shell", path: "provision.sh"


  config.vm.provision "shell", privileged: false, inline: "ssh-add -L >> ~/.ssh/authorized_keys"
  config.vm.provision "shell", inline: "sudo apt-get -y install python python-apt"







  config.vm.provision "ansible" do |ansible|
    ansible.inventory_path = "./ansible_hosts"
    ansible.limit = "fabisinatra"
    ansible.playbook = "sinatra.yml"




  end


#  config.vm.provision "shell", privileged: false, inline: <<-SHELL
#
#  echo "Provisioning Application and environment setup... please wait"
#  sudo apt-get updat >/dev/null 2>&1
#
#  echo "Installing ruby..."
#  sudo apt-get -y  install ruby >/dev/null 2>&1
#
#  echo "Installing git..."
#  sudo apt-get -y  install git >/dev/null 2>&1
#  
#  echo "Installing Bundler..."
#  sudo apt-get -y  install bundler --fix-missing >/dev/null 2>&1
#
#
#
#  mkdir -p ~ubuntu/.ssh
#  chmod 700 ~ubuntu/.ssh
#  echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDSCKg8fh8XBwpl0bEsQafiSvmaDAyDHWLA9aAu/HTobihN+E3XRexLQdVNg5XljCfOQVMivIFPAVAW1asft+uAWOYxTo9i09S34/GntJATXZNRHhtxc/yVoiwJ3hJy9ZgGnmee/XthfutBFG0Dh6aVbwfJQ0iNFBEEPAS7RYv7wtmN+rWHHJBkWHnuSFYkITdFd27YJgRsznUdGA8xrKF1qSVrO1VqSs2SK0Eom2QjlOL8yTa3T3i4fXDO2m56bSkTN9HYCmejoRYZ9WSSyGqoJzbjPH0aXYqTJ0bQzNSNlzwSFaytDPsxQNEFXasQW/Hgvx3+O5uSIXBqx4QEywZ5 ubuntu@ubuntu-xenial" > ~ubuntu/.ssh/id_rsa.pub
#  chmod 644 ~ubuntu/.ssh/id_rsa.pub
#
#  echo "-----BEGIN RSA PRIVATE KEY-----
#MIIEpQIBAAKCAQEA0gioPH4fFwcKZdGxLEGn4kr5mgwMgx1iwPWgLvx06G4oTfhN
#10XsS0HVTYOV5YwnzkFTIryBTwFQFtWrH7frgFjmMU6PYtPUt+Pxp7SQE12TUR4b
#cXP8laIsCd4ScvWYBp5nnv17YX7rQRRtA4emlW8HyUNIjRQRBDwEu0WL+8LZjfq1
#hxyQZFh57khWJCE3RXdu2CYEbM51HRgPMayhdaklaztVakrNkitBKJtkI5Ti/Mk2
#t094uH1wztpuem0pEzfR2Apno6EWGfVkkshqqCc24zx9Gl2KkydG0MzUjZc8EhWs
#rQz7MUDRBV2rEFvx4L8d/jubkiFwaseEBMsGeQIDAQABAoIBAQCKc3x7C+RwqIp5
#HeY9tzX03Nl2a5Tf5UIQ0pl5/58NDHhzFUgyrPwbi9UQ2Lm57E7dDoC/+CUBMGtb
#8hNwwCt0mqV7QT8RtXOWmKLWmxcSPO/8W+1ZN0z8Uj/XbVUaBLznOAo0awGm/iQT
#7WQDHKt5/AvU5w5vORgSg4HW9PxWwyQudG1v21st3TVmD8xd044e90Am4GhEzGKb
#O+OOFj4hIsGXfIo9BJedVKnEgiVsajqdPc2GIk1U1a5XUqG6h45MP9lm874sTgw3
#xn+FEfK7+ZMaH0gN8Crt/x2+/i9h0z/nCahwNwlMXoQeHlVbYNN0zOuewqJc87gk
#CuF2FA71AoGBAOpAO2ATE4TqsPPPPsvSCLwaIEfC9nijn1Oq1Ppnz4ykkbzP0VHS
#wsMblJyhwYjWJ3qNN5n4eF4jOpN27neIgL7BJlxwPvrQBdbhYYF5y+ZddZ7/Xw+I
#hqnrEXAp8J3Fe/e2iGSQWbxYTcCX2OD0cmGEtu0x0sQkeHzdw5jQTgEfAoGBAOWI
#0utPEMigBYXskO+l4X14qfJ0f6x3Iz8+U1M1/6Ok0IsxyUFDpBoGWjR5mfibqula
#v8B6dSpi5diyliKcd0yOdoTigUfonK8POSlZsvwcltmLMG3ymCXf74MS5kwmZlw4
#FSzLg5lfkphqO6+m76sfYRrGMqM5gCzreOWTZg1nAoGBAIf6bz0O9cazYbK1vBMe
#whlG5TQi9WYEPSmZQfZ1qmJO6ZZ74FsqCAqwCO1/bFPdVJ9sODl1pZGny4nsgPL8
#VxfkETuZoMWBWdJplGtPY1A/MlbwkKL4sosSPFYq0lUTXSnnWHdf3+dYLxI8UxYK
#cBcxreo0gM+BCDwbkz4ytQUrAoGAbeWupr86V/RV8KMtWbBgYASvycgBgP+hvpwG
#pSaLeTxmJN73buoF3fgApHM8Rw2xLP0oJe37vwmO5svKmlOzwtHK6SDRqS40JpTx
#V1z9FzxQ9WNxEpM+SZQIRwd7gCY6iBjJ+qKOJZbex17FqPoScioaAgm3IPNc7STo
#w3JpQC0CgYEA3seNvwXQ65ap+aCng3GY7QuD6D9weV/0ln+CKEFxvWjVEOKEm7Fj
#q3AUv0kac2zQXatVlPczwcVivQZxFXL3pNblHezdirOHR7jjLqlMLGP7DSzkVChz
#uU/3sv6/j+JVczbRw3wVs9D4dltypwUHTmikwaCBcuhfuMJzTsgJf9w=
#-----END RSA PRIVATE KEY-----" > ~ubuntu/.ssh/id_rsa
#  chmod 600 ~ubuntu/.ssh/id_rsa
#
#
#  ssh-keyscan -H github.com >> ~ubuntu/.ssh/known_hosts
#
#
#  git config --global user.name "localuser"
#  git config --global user.email "localuser@localhost" 
#
#
#
#  echo "Cloning Github repo..."
#  git clone git@github.com:rea-cruitment/simple-sinatra-app.git
#
#  echo "Installing Sinatra App..."
#  cd ./simple-sinatra-app
#  sudo bundle install
#
#  echo "Executing Sinatra App..."
#  sudo bundle exec rackup -D -p 80 -o 192.168.100.101
#
#
#
#  echo "Securing the Server..."
#
#  #Securing Shared memory
#  echo "tmpfs /run/shm tmpfs defaults,noexec,nosuid 0 0" >> sudo tee /etc/fstab
#  sudo mount -o remount -a
#
#  #Enable ssh login for specific users
#  echo "AllowUsers ubuntu" >> sudo tee /etc/ssh/sshd_config
#  sudo systemctl reload sshd.service
#
#
#  #Adding a security login banner and not showing kernel version at ssh sessions - with taking backup from the original files modified
#  echo "*** Authorized use only ***" > sudo tee /etc/issue.net
#  sudo sed -i.bak 's/^#Banner/Banner/' /etc/ssh/sshd_config
#  sudo sed -i.bak '$s/^/#/' /etc/update-motd.d/00-header
#  sudo systemctl reload sshd.service
#
#  # Hardening the Network layer
#  sudo sed -i.bak '/net.ipv[46].conf.all.accept_redirects/s/#net.ipv/net.ipv/' /etc/sysctl.conf
#  sudo sysctl --system >/dev/null 2>&1
#
#  # Enabling Host-based Firewall Service and only allow incomming TCP sessions to port 80 as per Applications requirements
#  sudo apt-get -y install firewalld >/dev/null 2>&1
#  sudo firewall-cmd --add-port=80/tcp
#
#  echo "All Done! - How to use: on the Host machine, from commandline, type in: lynx 192.168.100.101"
#
#
#
#
#  SHELL
end
