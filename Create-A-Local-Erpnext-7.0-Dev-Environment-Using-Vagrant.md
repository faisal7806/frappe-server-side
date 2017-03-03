### Create A Local Erpnext 7.0 Dev Environment Using Vagrant
#### Works on OSX, Linux and Windows. 

Sometimes it may be better to run your local Dev ERPNext instance in a VM instead of installing it directly on your local machine. This way if a problem arises with a ERPNext instance you can just delete the VM and recreate a new one without affecting the host OS. You can also run several different versions of ERPNext and various other software projects without having to worry about them interfering with each other. Using Vagrant allows us to manage various different VM's with minimal effort.


If you run a Mac I recommend installing **iTerm2** as a replacement to the default native OSX Terminal App: [https://www.iterm2.com](https://www.iterm2.com)


If your host Dev machine runs either **Mac** or **Windows** then check out **Vagrant Manager.** It is an excelent OSX Menu Bar / Windows Task Bar VM utility.
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
$ vagrant
```

You should see something like this:

```
Usage: vagrant [options] <command> [<args>]

    -v, --version                    Print the version and exit.
    -h, --help                       Print this help.

Common commands:
     box             manages boxes: installation, removal, etc.
     connect         connect to a remotely shared Vagrant environment
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login           log in to HashiCorp's Atlas
     package         packages a running vagrant environment into a box

     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     vbguest
     version         prints current and latest Vagrant version

For help on any individual command run `vagrant COMMAND -h`

Additional subcommands are available, but are either more advanced
or not commonly used. To see all subcommands, run the command
`vagrant list-commands`.

```

We now want to install the **Vagrant vbguest** plugin.  This plugin allows the Host and Guest machines to share files by installing **VirtualBox Guest Additions** onto all Guest machines.

```
$ vagrant plugin install vagrant-vbguest

```

## Create local ERPNext project folder
Create a folder in your local user root directory and name it something that makes sense to you. For example:  **erp_v7_001**

Copy the **ERPNext-Vagrant.box** file from your downloads folder into your new VM instance folder.

In your terminal navigate into your new VM instance folder :

```
$ cd ~/erp_v7_001

```

And then add the Vagrant Box.

```
$ vagrant box add ERPNext-Vagrant.box --name=erp_v7_001

```

Now issue the command `vagrant init`

```
$ vagrant init  
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant. 

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
  config.vm.box = "erp_v7_001"
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
The changes we added to the vagrant file are:

1: We want to use the **erp_v7_001** box

2: We wish to ssh into our VM with the **username frappe** and **pass frappe**

3: We have asigned an IP of 192.168.50.5 to this VM. We could have commented this line out and just used DHCP instead.

4: The NAT adaptor stuff is just a VirtualBox "bug" work around.

5: We increased the VM alotted memory from 1024MB to 2048MB. This speeds up ERPNext response time.

**IMPORTANT TO NOTE** that in this vagrantfile the **synced_folder line is currently commented out**. This is because when Vagrant sets up its shared folders it gives priority to the host machine which of course is empty.

To avoid issues it is important that we do the following. First ssh into our VM and move all the ERPNext files that we want to access on our Host machine to another temp folder. Then we uncomment the **synced_folder** line and save the vagrantfile. Then restart (aka reload in vagrant speak) the VM. Lastly once reloaded we will ssh back into our VM and copy back all the ERPNext files to their original folder. This way they will appear in our host machines shared folder and can be accessed on our MAC/PC/Linux Dev machine. 
Clear as mud? Just follow along and it will all make sense.


From within your project folder issue the command `vagrant ssh`

```
$ vagrant ssh  
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.13.0-79-generic i686)

 * Documentation:  https://help.ubuntu.com/
New release '16.04.2 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


 ERPNext Development VM (built on January 22, 2017)

 Please access ERPNext by going to the frappe-bench folder and running
 Access from : http://localhost:8000 on the host system. Use port 3022 for SSH.

 We provide rock solid hosting for ERPNext : erpnext.com/pricing

 To update, login as
 username: frappe
 password: frappe

 ERPNext Administrator Login:
 username: Administrator
 password: admin

 cd frappe-bench
 bench update

Last login: Wed Feb 24 11:41:18 2016
frappe@erpnext:~$

```
We are now logged into our VM as user frappe. The `ls` command will 
list all files and folders.

```
frappe@erpnext:~$ ls
bench-repo  frappe-bench  tmp
frappe@erpnext:~$

```

Issue the command
 `sudo mv /home/frappe/frappe-bench /home/frappe/frappe-bench-TMP/`

Once completed uncomment the synced_folder line in the vagrantfile. (Line 40) and resave the vagrantfile.

Open a new terminal window and navigate to your Host machine project folder `cd ~/erp_v7_001`

Issue the command `vagrant reload`

Once reloaded SSH back into your VM with `vagrant ssh`

Then issue the command

`sudo mv /home/frappe/frappe-bench-TMP/* /home/frappe/frappe-bench/`

This will take a few minutes to copy over and start to appear in your host machines shared folder. 

You should now `cd frappe-bench` and `bench update` 

Just ignore all the SNIMissingWarnings. I will write add more to this tutorial when I find the best solution.

Once completed you can issue the command `bench start` and point your web browser at `http://localhost:8080` and complete your ERPNext initial setup.

You can create as many VM's as you like this way. Just create a new project folder at say `~/erp_v7_002` in terminal `cd ~/erp_v7_002` issue `vagrant box add ERPNext-Vagrant.box --name=erp_v7_002` change the line `config.vm.box = "erp_v7_002"` in the vagrantfile etc etc.
