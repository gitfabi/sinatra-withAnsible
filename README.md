REA Systems Engineer practical task
===================================

Instructions for the reviewer
-----------------------------

To run this code, it needs to:
1 - Prepare Host environment outlined in "Requirements for running" section
2 - Log in as either normal user or root - for this solution username 'localuser' has been created and used all along with sudo capability
3 - Retrieve Git repository file:
  shell $ cd ~
  shell $ git clone git@github.com:gitfabi/updated-with-Ansible.git

4 - Deploy the Guest OS and provisioning: 
  shell $ cd sinatra-withAnsible
  shell $ vagrant up
5 - To test the application running:
  shell $ lynx 192.168.100.101    

6 - To repeat the build process:
    change directory to 'sinatra-withAnsible'
    shell $ vagrant destroy
    shell $ vagrant up

All provisioning tasks are taken care of within Vagrantfile, after guest OS creation.


Requirements for running
------------------------

System Requirements - packages and their dependencies:

- Host OS: CentOS 7.3

- Installing Git
  $ sudo yum -y install git

- Desktop Virtualization using VirtualBox on CentOS 7.3
  To allow VirtualBox utilize hardware resources from the Host OS, it's needed to have CPU/MMU Virtualization enabled (Intel VT-x/AMD-V) in BIOS. 
  If Host OS is running in VMWare or similar products, then consult relevant documents from official web-site to enable nested virtualization.
                
  $ cd /etc/yum.repos.d/
  $ sudo wget http://download.virtualbox.org/virtualbox/rpm/rhel/virtualbox.repo
  $ sudo yum -y install VirtualBox-5.1

  * Rebuild kernel modules with following command - it needs the epel repository to be added first:
  $ sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
  $ sudo yum -y install binutils gcc make patch libgomp glibc-headers glibc-devel kernel-headers kernel-devel dkms
  * Now we are ready to Build VirtualBox kernel modules
  $ sudo /usr/lib/virtualbox/vboxdrv.sh setup

  * Add VirtualBox User(s) to vboxusers Group - substitue 'localuser' with the username currently logged in
  $ sudo usermod -a -G vboxusers localuser

- Installing Vagrant
  $ sudo rpm -Uvh https://releases.hashicorp.com/vagrant/1.9.7/vagrant_1.9.7_x86_64.rpm

- Installing Ansible
  $ sudo yum -y install ansible

- Installing lynx
  $ sudo yum -y install lynx



Explanation of assumptions and design choices
---------------------------------------------

- This solution is tested on CentOS 7.3-x_64 built from the scratch and should be portable to other Linux distributions. However, to satisfy software requirements on the Host machine other than CentOS/RHEL/Fedora, some modifications are needed for package installation, software repository and commands used in this document.

- It's assumed either 'root' user is used for package installation, or normal user has enough 'sudo' privilege to install applications on the Host machine


- The Guest Operating System is Ubuntu 16.04 - the instance name is "ubuntu/xenial64", taken from Vagrant repository, and the URL is: "https://app.vagrantup.com/ubuntu/boxes/xenial64"

- To secure the application server, 'firewalld' service has been used. Alternatively, IPTables can be used.

- Privat IP address of 192.168.100.101 is allocated for the guest machine. If this IP conflicts with your existing private IP settings, please substitue it with another IP in the follwoing files:
	Vagrantfile
	ansible_hosts
	sinatra.yml

- To make deployment easier, codes for runnign application provided by REA is automatically retrieved from Git repositoy. To do so, localuser user's public and private key is copied in ~ubuntu/.ssh folder to skip SSH key import required by 'git clone' for the newly created user in the guest OS. Alternitavely, REA code can be retrieved in the Vagrant's shared folder to avoid sharing RSA key with the rest of the world!


- To secure the application server below steps are taken:
  * Securing Shared memory
  * Enable ssh login for specific user, i.e. 'ubuntu'
  * Not showing kernel version at ssh sessions
  * Hardening the Network layer
  * Enabling Host-based Firewall Service and only allow incomming TCP sessions to port 80 as per Applications requirements

  Other security mechanism can also be implemented, such as:
  * Password protecting GRUB menu
  * SELinux
  * Auditing
  * Allowing/Disallowing non-admin users' access to certain commands via sudo file
  * Restricting SHH/HTTP/etc services to certain IP ranges, using Host-based Firewall already installed

