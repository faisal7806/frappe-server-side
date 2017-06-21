### Create A Local Erpnext 7.0 Dev Environment Using Vagrant
#### Works on OSX, Linux and Windows. 

Sometimes it may be better to run your local Dev ERPNext instance in a VM instead of installing it directly on your local machine. This way if a problem arises with a ERPNext instance you can just delete the VM and recreate a new one without affecting the host OS. You can also run several different versions of ERPNext and various other software projects without having to worry about them interfering with each other. Using Vagrant allows us to manage various different VM's with minimal effort.


If you run a Mac I recommend installing **iTerm2** as a replacement to the default native OSX Terminal App: [https://www.iterm2.com](https://www.iterm2.com)


If your host Dev machine runs either **Mac** or **Windows** then check out **Vagrant Manager.** It is an excellent OSX Menu Bar / Windows Task Bar VM utility.
[http://vagrantmanager.com](http://vagrantmanager.com)

## ERPNext Vagrant Setup Requirements

Download **ERPNext Vagrant Box** from:
[https://erpnext.com/download](https://erpnext.com/download)

Download and install **VirtualBox** from:
[https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads)

Download and install **Vagrant** from:
[https://www.vagrantup.com](https://www.vagrantup.com)

To check that vagrant was installed open your terminal App and enter:

`$ vagrant`

Install the Vagrant vbguest plugin. It allows the Host and Guest machines to share files and folders.

`$ vagrant plugin install vagrant-vbguest`

Create a local ERPNext project folder in your local user root directory and give it your project name. For example:  erp_v801

Copy the ERPNext-Vagrant.box file from your downloads folder into this ~/erp_v801.

In your terminal navigate into your new project folder :

`$ cd ~/erp_v801`

Add the Vagrant Box.

`$ vagrant box add ERPNext-Vagrant.box --name=erp_v801`

Issue the command vagrant init

`$ vagrant init`

`$ A Vagrantfile has been placed in this directory.`

Open up the newly created vagrantfile in your text editor, Select all the text and delete it. Replace it with the text below and then save the file.

```
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
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "erp_v801"
  config.ssh.username = "frappe"
  config.ssh.password = "frappe"


  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 8000, host: 8080
  config.vm.network "forwarded_port", guest: 3000, host: 3000

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.50.5"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  #config.vm.synced_folder ".", "/home/frappe/frappe-bench/"
  #
  #
  config.vm.provider "virtualbox" do |vb|
  # Display the VirtualBox GUI when booting the machine
  # vb.gui = true

  ### Change network card to PCnet-FAST III
  # For NAT adapter
  vb.customize ["modifyvm", :id, "--nictype1", "Am79C973"]
  # For host-only adapter
  vb.customize ["modifyvm", :id, "--nictype2", "Am79C973"]
  # Customize the amount of memory on the VM:
  vb.memory = "2048"
  end

end
```


The changes we added to the default vagrant file were:

1: We want to use the erp_v801 box

2: We wish to ssh into our VM with the username frappe and pass frappe

3: We have asigned an IP of 192.168.50.5 to this VM. By default this line is ommented out and uses DHCP instead.

4: The NAT adaptor stuff is just a VirtualBox bug work around.

5: We increased the VM alotted memory from 1024MB to 2048MB. This speeds up VM App response time.

6: In this vagrant file the SYNCED_FOLDER line is currently commented out.

This is because when Vagrant sets up its shared folders it gives priority to the host machine.

To avoid issues with the ERPNext vagrant box which has Frappe and ERPNext preinstalled on it. We need to move all the preinstalled ERPNext files to a temp folder within the VM. 

From within your Host Machine project folder issue the command `vagrant up`

Once the VM is Up issue `vagrant ssh`

Logged into our VM as user frappe. The `ls` command will list current directory files and folders.

```
frappe@erpnext:~$ ls
bench-repo  frappe-bench  tmp
frappe@erpnext:~$
```
Issue the commands.

```
frappe@erpnext:~$ sudo mv /home/frappe/frappe-bench /home/frappe/frappe-bench-TMP002/ 
frappe@erpnext:~$ mkdir frappe-bench
```
Password for sudo: frappe

Password for SQL root: frappe

Once completed, 

Uncomment the synced_folder line in the vagrant file. (Line 40) in your text editor and save the vagrantfile.

On your Host Machine `cd ~/erp_v8_001`

Issue the command `vagrant reload`

Once reloaded  `vagrant ssh`

```
sudo mv /home/frappe/frappe-bench-TMP002/* /home/frappe/frappe-bench/
```

This will take a few minutes to copy the files over and start to appear in your Host machines shared folder. 

Once completed `cd frappe-bench` and `bench update`

Currently just ignore all the SNIMissingWarnings untill someone finds a fix.

Once ERPNext is up to date issue the command `bench start` and point your web browser at http://localhost:8080 and begin  your ERPNext initial setup.

You can create as many VM’s as you like this way. Just create a new project folder at say `~/erp_v802`

```
cd ~/erp_v802

vagrant box add ERPNext-Vagrant.box --name=erp_v802

vagrant init

vagrant up

vagrant ssh

```