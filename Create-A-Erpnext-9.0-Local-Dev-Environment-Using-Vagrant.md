### Create A Local ERPNext 9.0 Dev Environment Using Vagrant
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

```
$ vagrant --version
```

We now want to install the **vbguest** plugin. This plugin allows the Host and Guest machines to share files by installing **VirtualBox Guest Additions** onto all future guest machines.

```
$ vagrant plugin install vagrant-vbguest
```

## Create local ERPNext project folder
Create a project folder in your local user root directory and name it something that makes sense to you. For example:  **~/erp_v9_001**

Copy the **ERPNext-Vagrant.box** file from your downloads folder into this folder.

Open your terminal and navigate into your new project folder :

```
$ cd ~/erp_v9_001

```

And then add the Vagrant Box.

```
$ vagrant box add ERPNext-Vagrant.box --name=erp_v9_001

```

Now issue the command

```
$ vagrant init 

```
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
  config.vm.box = "erp_v9_001"
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
  # config.vm.network "private_network", ip: "192.168.50.5"

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
The important changes we made to the vagrant file are:

1: We want to use our **erp_v9_001** box

2: We want to ssh into our VM with the **username frappe** and **pass frappe**

3: We could assign an IP of say 192.168.50.5 to this VM by uncommenting the line `# config.vm.network "private_network", ip: "192.168.50.5"` Instead we are just using DHCP.

4: The NAT adaptor stuff is just a VirtualBox "bug" work around.

5: We increased the VM alotted memory from 1024MB to 2048MB. This speeds up ERPNext response time.

**Important to note** is that in our vagrant file the **SYNCED_FOLDER** line is currently commented out. This is because when Vagrant sets up its shared folders it gives priority to the Dev host machine which is currently empty.

From within your local project folder `~/erp_v9_001` issue the command `vagrant up`

Once the VM is up issue the command `vagrant ssh`

We are now logged into our VM as user frappe.
The `ls` command will list current directory files and folders.

```
frappe@erpnext:~$ ls
bench-repo  frappe-bench  tmp
frappe@erpnext:~$

```

Issue the command

```
sudo mv /home/frappe/frappe-bench /home/frappe/frappe-bench-TMP/

```

Once all the files have been moved
**Uncomment the synced_folder line in the vagrant file.** (Line 40) and save the vagrantfile.

Open a new terminal window and navigate to your Local Host machine project folder `cd ~/erp_v9_001` then `vagrant reload`

Once reloaded SSH back into your VM with `vagrant ssh`

Then issue the command

`sudo mv /home/frappe/frappe-bench-TMP/* /home/frappe/frappe-bench/`

This will take a few minutes to copy all the ERPNext files into your Local Host machines project folder.
Once completed update Ubuntu with `sudo get-apt update` then `cd frappe-bench` and `bench update` 

Currently just ignore any SNIMissingWarnings.

Once ERPNext is up to date issue the command `bench start` from VM frappe-bench folder and point your web browser at `http://localhost:8080` and start your initial ERPNext setup.

The command `vagrant halt` from your Local Dev machine project folder will shut down the VM.

You can create as many seperate VM's on your Local Dev machine as you like. Just create a new project folder `~/erp_v9_002` and copy and paste our previous Vagrant file and ERPNext-Vagrant.box into it. Change `config.vm.box = "erp_v9_001"` to `config.vm.box = "erp_v9_002"` and comment out the shared folder line in the vagrant file then save it.

```
$ cd ~/erp_v9_002
$ vagrant box add ERPNext-Vagrant.box --name=erp_v9_002
$ vagrant init
$ vagrant up
$ vagrant ssh

```