# Vagrant V5 box installation instructions:
This box already has all dependencies (except wkhtmltopdf - i forgot). One database, **site1.local**, is installed by default. Mysql root password is `frappe@` and Administrator password is `frappe@`. User frappe is not necessary because frappe was installed with user vagrant with no password. But if you must to know user frappe password is `frappe@`. 

Here is the link: [Vagrant box](https://meocloud.pt/link/c32bc5b3-9197-4654-971c-483d1d8ecbeb/frappe_v5/)

If any one of the community wants to try it is very simple, justo a few steps:

1. first you have to install [Virtualbox](https://www.virtualbox.org) if it isn't already installed!
2. then install vagrant from [Vagrant Home Page](https://www.vagrantup.com).
3. then download my box file and Vagrantfile from [Vagrant box](https://meocloud.pt/link/c32bc5b3-9197-4654-971c-483d1d8ecbeb/frappe_v5/) to any directory, and inside that directory make another empty directory with the name **erpnext** (it has to have this name. But you can change it in Vagrantfile that is included in download).

[Like this](https://meocloud.pt/link/8912640b-b828-4e96-b26a-5304b988375b/setup_v5_img.png/)

4. then issue the following command, after download: **vagrant box add frappev5 frappe_erpnext_v5.box**. frappev5 is the title at your choice but if you change it you have to change it in Vagrantfile too. The second name is the name of my box, frappe_erpnext_v5.box.
5. After that command you have to issue **vagrant up** and then wait, after that frappe is ready to start.
6. Do, **vagrant ssh** to enter in vagrant virtual machine (ubuntu 14.10 in this case...).
7. after vagrant ssh you are in virtual machine inside the shared directory. This directory is shared with the host machine (mac or windows). **Note:** there is one identically directory in **/home/vagrant** (named, frappe-bench and another named bench-repo) but these are just the prototypes (things that have to do with vagrant itself...) the one that you have to use is in **/vagrant/frappe-bench** directory and is the one that you work in the host machine and share with the guest machine.
8. some important commands: `vagrant reload`; `vagrant halt`; `vagrant provision`; and you can change the memory used by guest machine in Vagrantfile.

**Note:** Vagrant is in production with nginx and supervisor installed and working. The first time that you install and make `vagrant up` nginx is not working properly, you have to issue `sudo /etc/init.d/nginx restart` to refresh.
After that nginx and supervisor will start properly. If you want to turn of nginx and supervisor when you start vagrant edit the file in /home/vagrant/.bashrc and comment `sudo supervisorctl reread` and `sudo supervisorctl update`.

Resume: if you already have installed virtualbox and vagrant you just have to download my box and make the erpnext directory, issue **vagrant box add frappev5 frappe_erpnext_v5.box**, **vagrant up** and **vagrant ssh**.

In the erpnext directory my box will make the frappe-bench directory with frappe and bench already configured. This is the directory that you use in the host machine and share with the guest machine. This way you don't have to open virtualbox gui of the guest machine that is heavy, and you develop always with native app of host machine. The ports are forwarded in Vagrantfile and we access the frappe desk with host browser, with web server nginx -> `http://localhost:8020`, the same to mysql or if you want start `bench serve --port=8030`, just see Vagrantfile.

This ideal for windows and mac developers.

### For Windows you have to install PuTTY or other.
You can't do vagrant ssh. 

The authentication information is:

Host: 127.0.0.1

Port: 2222

Username: vagrant

Password: vagrant

or

Import the private key: C:/Users/Your Name/.vagrant.d/insecure_private_key

Good luck!!!