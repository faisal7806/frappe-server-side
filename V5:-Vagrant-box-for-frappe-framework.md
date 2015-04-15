# Vagrant V5 box installation instructions:
This box already has all dependencies. One database, **site1.local**, is installed by default. Mysql root password is `frappe@` and Administrator password is `frappe@`. User frappe is not necessary because frappe was installed with user `vagrant` and password `vagrant`. But if you must to know user frappe password is `frappe@`. 

Here is the link: [Vagrant box](https://meocloud.pt/link/c32bc5b3-9197-4654-971c-483d1d8ecbeb/frappe_v5/)

If any one of the community wants to try it is very simple, justo a few steps:

1. first you have to install [Virtualbox](https://www.virtualbox.org) if it isn't already installed!
2. then install vagrant from [Vagrant Home Page](https://www.vagrantup.com).
3. then download my box file and Vagrantfile from [Vagrant box](https://meocloud.pt/link/c32bc5b3-9197-4654-971c-483d1d8ecbeb/frappe_v5/) to any directory, and inside that directory make another empty directory with the name **erpnext** [Like this](https://meocloud.pt/link/a20b19b2-50d3-46c1-9b6d-976869e0185c/erpnext_dir.png/) (it has to have this name. But you can change it in Vagrantfile that is included in download).

4. After download, issue the following command: **vagrant box add frappeV5 frappe_erpnext_v5.box**.
5. After that command you have to issue **vagrant up** and then wait; then, frappe is ready to start.
6. Do, **vagrant ssh** to enter in vagrant virtual machine (ubuntu 14.10 in this case...). But, it is not necessary to access frappe.
7. After vagrant ssh you are in virtual machine inside the shared directory. This directory is shared with the host machine (mac or windows). **Note:** there is one identically directory in **/home/vagrant** (named, frappe-bench and another named bench-repo) but these are just the prototypes (things that have to do with vagrant itself...) the one that you have to use is in **/vagrant/frappe-bench** directory and is the one that you work in the host machine and share with the guest machine.
8. Some important commands: `vagrant reload`; `vagrant halt`; `vagrant provision`; and you can change the memory used by guest machine in Vagrantfile.

**Note:** Vagrant is in production with nginx and supervisor installed and working. You don't have to do `vagrant ssh` to start nginx, supervisor and guinicorn. After you issue `vagrant up` you can, from the host browser, access frappe framework, just do: `http://localhost:8020`.
If you want to turn off nginx and supervisor when you start vagrant, comment `sudo supervisorctl reread` and `sudo supervisorctl update` in Vagrantfile.

Resume: if you already have installed virtualbox and vagrant you just have to download my box and make the erpnext directory, issue **vagrant box add frappeV5 frappe_erpnext_v5.box**, **vagrant up** and to access frappe point the host browser to `http://localhost:8020`. If you wish to login issue: **vagrant ssh**.

In the erpnext directory my box will make the frappe-bench directory with frappe and bench already configured. This is the directory that you use in the host machine and share with the guest machine. This way you don't have to open virtualbox gui of the guest machine that is heavy, and you develop always with native app of host machine. The ports are forwarded in Vagrantfile and we access the frappe desk with host browser: with web server nginx on -> `http://localhost:8020` or if you want start web server: `bench serve --port=8030`, the same to access mysql, just see Vagrantfile for the forwarded ports.

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