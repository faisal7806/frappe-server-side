# Vagrant box installation instructions:
This box already has all dependencies installed and i git cloned erpnext and shopping cart. These apps are ready to install but already in vagrant file. Just need to issue **bench frappe --install_app erpnext site1.local** and **bench frappe --install_app shopping_cart site1.local**. One database, **site1.local**, is installed by default. Mysql root password is erpnext.

Here is the link: [Vagrant box](https://meocloud.pt/link/a6fdac48-bdf2-4fb7-b87b-4a300188a6b8/vagrant-frappe/)

If any one of the community wants to try it is very simple, justo a few steps:

1. first you have to install [Virtualbox](https://www.virtualbox.org) if it isn't already installed!
2. then install vagrant from [Vagrant Home Page](https://www.vagrantup.com).
3. then download my box file [Vagrant box](https://meocloud.pt/link/a6fdac48-bdf2-4fb7-b87b-4a300188a6b8/vagrant-frappe/) and unzip it to any directory, and inside that directory make another empty directory with the name **erpnext** (it has to have this name. But you can change it in Vagrantfile that is included in download).

4. then issue the following command, after download: **vagrant box add frappe-erpnext-vagrant-box frappe-erpnext.box**. frappe-erpnext-vagrant-box is the title at your choice but if you change it you have to change it in Vagrantfile too. The second name is the name of my box, frappe-erpnext.box.
5. After that command you have to issue **vagrant up** and then wait, after that frappe is ready to start.
6. Do, **vagrant ssh** to enter in vagrant virtual machine (ubuntu 14.04 in this case...).
7. after vagrant ssh you are in virtual machine, do **cd /vagrant/frappe-bench** to change directory and **bench start** to go. This directory is the shared directory with the host machine (mac or windows). **Note:** there is one identically directory in **/home/vagrant** (named, frappe-bench) but that is just the prototype (things that have to do with vagrant itself...) the one that you have to use is in **/vagrant/frappe-bench** directory and is the one that you work in the host machine and share with the guest machine.
8. some important commands: vagrant reload; vagrant halt; and you can change the memory used by guest machine in Vagrantfile.

Resume: if you already have installed virtualbox and vagrant you just have to download my box and make the erpnext directory, issue **vagrant box add frappe-erpnext-vagrant-box frappe-erpnext.box**, **vagrant up** and **vagrant ssh**.

In the erpnext directory my box will make the frappe-bench directory with frappe and bench already configured. This is the directory that you use in the host machine and share with the guest machine. This way you don't have to open virtualbox gui of the guest machine that is heavy, and you develop always with native app of host machine. The ports are forwarded in Vagrantfile and we access the frappe desk with host browser, `http://localhost:8000` or if you prefer in this case `http://33.33.33.10:8000` the same to mysql, just see Vagrantfile.

This ideal for windows and mac developers.

Here is my desktop:

[Desktop vagrant in action...](https://meocloud.pt/link/703a0b49-9a4f-404e-b77b-29416d77cacb/vagrantBox.png/)

### For Windows you have to install PuTTY or other.
You can't enter vagrant ssh, and enter the following:

Host: 127.0.0.1

Port: 2222

Username: vagrant

Password: vagrant

or

Private key: C:/Users/Your Name/.vagrant.d/insecure_private_key

