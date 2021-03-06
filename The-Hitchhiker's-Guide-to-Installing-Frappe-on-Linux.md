> From Zero to Hero
>
> [Achilles Rasquinha](https://github.com/achillesrasquinha) <[achilles@frappe.io](mailto:achilles@frappe.io)>, [Ameya Shenoy](https://github.com/codingCoffee) <[ameya@frappe.io](mailto:ameya@frappe.io)>

To the best of our knowledge, this will be the only page you'd ever require to install [frappe](https://github.com/frappe/frappe) right from scratch. This script also believes to be a foolproof setup to have [frappe](https://github.com/frappe/frappe) onto your system. **In case if you run into some problems, feel free to raise an issue [here](https://github.com/frappe/frappe/issues)** with the title `[frappe-install]` followed by your issue. Your issue must have the following - System (OS) version, Dependency versions, Error Log.

**NOTE:** To see if your Linux OS distribution has been tested for the following script, check [here](#tried-and-tested). You're free to revise this page in order to add your Linux OS distribution if you're successful with this script too (_psst_, helps others).

**Note that** the method described here will install Frappe's developer branch/mode. If you want the stable production branch/are looking for a complete production setup, follow the [Easy Install](https://github.com/frappe/bench#easy-install) method.

#### Getting [Frappe](https://github.com/frappe/frappe) onto your system

Before going further, here's something you need to know. [Frappe](https://github.com/frappe/frappe) is not just a web framework as a whole but also an app itself.

##### Q. Wait, what's an app?

You can think of an app in the [Frappe](https://github.com/frappe/frappe) jargon as a collection of mutable definitions and custom functionalities for a said use-case (basically, a codebase). You then install such apps on sites (which consists of one database at a domain, files, etc.) that acts as the view layer to your app (just like any other website).

##### Q. Apps? Sites? Why would you do such a thing?

**Multi-tenancy**. [Frappe](https://github.com/frappe/frappe) was built with an intention for you to reuse a codebase, definitions, functions, views, etc. Both, apps and sites are contained within what we call as - _drum rolls_ - **the Bench!**

<p align="center">
    <img src="https://i.imgur.com/dZBThmp.png" height="150" alt="Bench: sites and apps"/>
</p>

You then manage your apps and sites within your Bench. To know more, click [here](https://www.youtube.com/watch?v=eCAMPcl7NKc&feature=youtu.be&t=32s) to completely know the architecture from the author of [frappe](https://github.com/frappe/frappe), [Rushabh Mehta](https://github.com/rmehta) himself.

##### Q. Apps? Sites? And now Bench?

Yes, the Bench! You can think of the bench as the guardian for both, your apps and sites. Bench is the heart and soul of apps and sites built using the [frappe](https://github.com/frappe/frappe) framework. You store, update, manage and mutate apps within your bench. Not just that > [`bench`](https://github.com/frappe/bench) is to frappe, what `apt-get` is to Debian-based Linux OS :wink:

We provide you the [`bench`](https://github.com/frappe/bench) command-line tool for you to create Benches, Apps and Sites. For installing apps built on Frappe, we use [`git`](https://git-scm.com) as our Source Control Manager (SCM) to have them fetched from remote repositories.
![](https://i.imgur.com/QwNrzPo.png)

To get to know more about **Bench**, check out [this](https://www.youtube.com/watch?v=GVWrKuj-EAc&feature=youtu.be&t=41s) talk from the author of [bench](https://github.com/frappe/bench) ([Pratik Vyas](https://github.com/pdvyas)).

### Installation

First, open your Terminal (`Ctrl` + `Alt` + `T`)

### Dependencies

- Install [`git`](https://git-scm.com)

  **Debian/Ubuntu**

```bash
sudo apt-get install git
```

- Check whether **git** has been installed correctly

```bash
git --version
```

You should then see `git version X.Y.Z` on your terminal screen.

- Pay careful attention to the Python version that you use in the following steps. Read the instructions first carefully before executing the commands.

[Frappe](https://github.com/frappe/frappe) requires at least Python 2.7 installed, but Python3.5+ also supported. To our luck, Python comes shipped with most Linux OS distributions. However, we might require the `python-dev` package installed for using Python's C API.

- To install Python 2.7.X `dev` package on your Linux OS, simply:

  **Debian/Ubuntu**

```bash
sudo apt-get install python-dev
```

Alternatively, to install Python 3.X `dev`:

```bash
sudo apt-get install python3-dev
```

- Install `setuptools` and `pip` (Python's Package Manager):

```bash
sudo apt-get install python-setuptools python-pip
```

Alternatively, for Python 3.X `setuptools` and `pip` (Python's Package Manager):

```bash
sudo apt-get install python3-setuptools python3-pip
```

Install `virtualenv`:

```bash
sudo apt-get install virtualenv
```

You can also create an alias for pip and python to enforce use of python 3:

```
alias python=python3
alias pip=pip3
```

[Frappe](https://github.com/frappe/frappe) uses [MariaDB](https://mariadb.org) (for [RDBMS](https://en.wikipedia.org/wiki/Relational_database_management_system)) as its database engine, [Redis](https://redis.io) for caching and as a message broker and [Node.js](https://nodejs.org) for everything JavaScript. Go ahead and install 'em all.

**Debian/Ubuntu**

- To install MariaDB 10.3 `stable` package on your Linux OS, simply:

```bash
sudo apt-get install software-properties-common
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
sudo add-apt-repository 'deb [arch=amd64,i386,ppc64el] http://ftp.ubuntu-tw.org/mirror/mariadb/repo/10.3/ubuntu xenial main'

sudo apt-get update
sudo apt-get install mariadb-server-10.3
```

During this installation you'll be prompted to set the MySQL root password. If you are not prompted for the same, you'll have to initialize the MySQL server setup yourself after the above command completes. You can initialize the MySQL server setup by executing the following command

```bash
sudo mysql_secure_installation
```

**Remember**: only run `sudo mysql_secure_installation` if you're not prompted the password during setup.

It is really important that you remember this password, since it'll be needed later on!
Test whether the installation has worked with `mysql -u root -p -h localhost`. You should be prompted for the mysql root password you have provided during the installation. Get back out of the mysql console by typing `\q`

Next you'll need the MySQL database development files

```bash
sudo apt-get install libmysqlclient-dev
```

You also need to edit the mariadb configuration (although the guide in README doesn't mention this, you'll face an error message asking you to do exactly this if you follow the README. So you might as well go ahead and do this)

```bash
sudo nano /etc/mysql/my.cnf
```

And add this to the file

```ini
[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

[mysql]
default-character-set = utf8mb4
```

_Note any includes that might overwrite these settings!_

(Now press (Ctrl-X) to exit!)
Finally restart the mysql server and you'll be good to go!

```bash
sudo service mysql restart
```

- To install Redis on your Linux OS, simply:

```bash
sudo apt-get install redis-server
```

- To install Node.js 12.X package on your Linux OS, simply:

```bash
sudo apt-get install curl
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
```

- Frappe uses `yarn` as a package manager. To install it, run

```bash
sudo npm install -g yarn
```

- If you intend to use the PDF generation functionality provided by frappe, you'll need to install `wkhtmltopdf`. You can download a package from [here](https://wkhtmltopdf.org/downloads.html). 

For **Ubuntu 18.04**, the installation will look like this:

```
wget https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6-1/wkhtmltox_0.12.6-1.bionic_amd64.deb
sudo apt install ./wkhtmltox_0.12.6-1.bionic_amd64.deb
rm wkhtmltox_0.12.6-1.bionic_amd64.deb
```

#### Create a user

Bench and frappe should run under a non-root user. If you are on a server, as root, create a new sudo user and switch to it. Change `my_user` to any username you like (`frappe` is a common choice, which makes it an attractive target for hackers).

```bash
adduser my_user
usermod -aG sudo my_user
su - my_user
```

#### Getting [Bench](https://github.com/frappe/bench) onto your system

```bash
sudo -H pip install frappe-bench
```

- Check whether **Bench** has been installed correctly (you may wish to log out and log back into your terminal before this step, as this will refresh your environment variable, adding ~/.local/bin to your path if it not already there)

- You must login / "su - your_user_id" using the user id which you have used to install **Bench**

```bash
bench --version
```

You should then see `X.Y.Z` on your terminal screen.

And there you have it! You're now ready to build something awesome using [frappe](https://github.com/frappe/frappe)

#### Bench - Quickstart

To create a new bench, simply use the `bench init` command as follows:

```bash
bench init [--frappe-branch <branch>] [--python <path to python executable>] <MY_BENCH>
```

By default `bench` would fetch from `develop` branch, So to install from latest stable ([`version-12`](https://github.com/frappe/frappe/tree/version-12)) branch or use [other branches](https://github.com/frappe/frappe/branches) to install older versions.

<small>This option is available only with `bench` installed through git. Latest release doesn't have this yet.

e.g.

```bash
bench init --frappe-branch version-12 frappe-bench
```

and for python 3:

```bash
bench init --frappe-branch version-12 --python /usr/bin/python3 frappe-bench
```

This goes ahead and creates a folder named `frappe-bench` with a whole lot of stuff inside! This might take a while (depending on your internet speed). We, at frappe love our coffee with flavour. Go get one brewed for yourself.

Once done, simply change to your bench directory:

```bash
cd <MY_BENCH>
```

e.g.

```bash
cd frappe-bench
```

To ensure python loads frappe properly, you might need to install the application as a python module:

```bash
./env/bin/pip install -e apps/frappe/
```

and for python 3:

```bash
./env/bin/pip3 install -e apps/frappe/
```

#### What should you see?

Typing an `ls` on your terminal, you should see the following:

```bash
├── 🗄️ apps               # frappe apps
├── 🗄️ config             # all configuration files (*.conf)
├── 🗄️ env                # virtual environment (an isolated python environment catering to python dependencies for frappe apps only)
├── 🗄️ logs               # all log files
├── 🗄️ node_modules       # collective node dependencies for frappe apps
├── 🗄️ sites              # frappe sites
├── 📁 package.json       # list of node dependencies
├── 📁 package-lock.json  # locking the list of node dependencies
├── 📁 patches.txt        # list of patches patched
├── 📁 Procfile           # process file (to let honcho activate a list of all processes)
```

#### Is your MariaDB not on the local server?

If you followed instructions above, you installed a local copy of MariaDB on your server. ERPNext will communicate with MariaDB via a Unix socket.

_However_, there are other deployment options for MariaDB:

- MariaDB is installed on a different machine.
- MariaDB is hosted on a virtual container, like Docker.

_If you need to communicate with MariaDB using TCP_, you have to make a quick change:

1. Edit this file: ../frappe-bench/sites/_common_site_config.json_
2. Add this line:

```
"db_host": "127.0.0.1"
```

Make sure you change the IP address to the correct value. It could be your localhost, or a virtual network, or the IP of a remote server.

By making this change, when you later try to start ERPNext --> it will connect to MariaDB using **TCP** to that address. Instead of searching for a local Unix socket (which it would not find, and throw an error)

Again, only make this change if you're _not_ using a local MariaDB installation.

---

**Caution:** _Before starting bench!_ If you are redoing previous installations, remove any browser tabs that might still be trying to open connections to the site you previously created. While it is not certain they will mess with your installation, you could see errors logged unrelated to your installation steps.

#### Start bench

Go ahead and start bench as follows:

```bash
bench start
```

#### Creating Sites

**NOTE:** You might need another terminal instance to run the following commands within the path to your `MY_BENCH` directory.

```bash
bench new-site <MY_SITE>
```

e.g.

**NOTE:** Remember to switch to `frappe-bench` subdirectory prior to running the command for creating site.

```bash
cd frappe-bench
```

```bash
bench new-site foo.bar
```

You'll be then prompted to type your MySQL root password (which then goes ahead and creates a new database for your site). You'd also be prompted to create a new password for the System Administrator. A site comes with frappe installed by default. Like I mentioned

> Frappe is not just a web framework as a whole but also an app itself.

#### Site based multi-tenancy

Frappe lets you create multiple sites, in a single instance. To enable site based multi-tenancy empty the contents of the file `currentsite.txt` using the text-editor of your choice (I'm using nano here)

```bash
bench config dns_multitenant on
nano sites/currentsite.txt
```

Then add an entry of the site you just created into the `/etc/hosts` file.

```bash
sudo nano /etc/hosts
```

Add the following line and save the file

```bash
127.0.0.1	foo.bar
```

_Note: If you skip this step or make a mistake doing it, you will see `socketio` throwing DNS errors in your bench log like this:_

```bash
15:30:50 socketio.1       | Unable to join chat room. Error: getaddrinfo EAI_AGAIN mysitefoo.bar:80
```

#### Fetching Frappe Apps

[ERPNext](https://erpnext.org) happens to be two things - a Frappe App and [the world's best 100% Open Source ERP](https://opensource.com/resources/top-4-open-source-erp-systems). You can have [erpnext](https://github.com/frappe/erpnext) fetched and stored within your bench using the following command:

```bash
bench get-app [--branch <branch>] <APP_REMOTE_URL|VALID_FRAPPE_APP>
```

If you don't want the `development` version, Specify the required branch.

e.g.

```bash
bench get-app --branch version-12 erpnext
```

This goes ahead and fetches the complete source code and places it within your `MY_BENCH/apps/MY_APP_NAME` folder. In this case - `frappe-bench/apps/erpnext`

To ensure python loads erpnext properly, you might need to install the application as a python module:

```bash
./env/bin/pip install -e apps/erpnext/
```

and for python 3:

```bash
./env/bin/pip3 install -e apps/erpnext/
```

#### Installing Frappe Apps onto Sites

```bash
bench --site <MY_SITE> install-app <MY_APP_NAME>
```

e.g.

```bash
bench --site foo.bar install-app erpnext
```

#### You're all set!

Now you can simply access the site you just created using this link in the browser [foo.bar:8000](http://foo.bar:8000)

#### Access your site from the outside

Not satisfied ? You want to be able to show your site to the world ? You can install NGinx and use bench to generate the configuration for you.

- Install nginx

```
sudo apt-get install nginx
```

- Generate nginx config for your site(s)

```
bench setup nginx
```

- Remove enable sites

```
rm -f /etc/nginx/sites-enabled/*
```

- Create symbolic link to nginx conf for frappe

```
sudo ln -s ./config/nginx.conf /etc/nginx/sites-enabled/frappe.conf
or if "sudo service nginx restart" failed because link is not exist
sudo ln -s /home/my_user_id/my_bench_folder/config/nginx.conf /etc/nginx/sites-enabled/frappe.conf
```

- Finally, restart nginx

```
sudo service nginx restart
```

You can now access your site at your server's IP address.

#### Tried and Tested

**NOTE:** If you're attempting to revise this page after successfully installing and running frappe, kindly add the required details in the following format only.

| Name             | Version                              | By                                                                                                                                                                                                                                                                                          |
| ---------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Ubuntu           | 16.04.1                              | Ameya Shenoy <br/> [@codingCoffee](https://github.com/codingCoffee), <<a href="mailto:ameya@frappe.io">ameya@frappe.io</a>>                                                                                                                                                                 |
| Ubuntu           | 16.04.5                              | Achilles Rasquinha <br/> [@achillesrasquinha](https://git.io/achilles), <<a href="mailto:achillesrasquinha@gmail.com">achillesrasquinha@gmail.com</a>>                                                                                                                                      |
| Ubuntu           | 18.04                                | Ameya Shenoy <br/> [@codingCoffee](https://github.com/codingCoffee), <<a href="mailto:ameya@frappe.io">ameya@frappe.io</a>>                                                                                                                                                                 |
| Ubuntu           | 18.04                                | Brian Pond <br/> [@PMojito](https://github.com/PMojito), <<a href="mailto:brian@pondconsulting.net">brian@pondconsulting.net</a>>                                                                                                                                                           |
| Ubuntu           | 18.04                                | Satadru Sengupta <br/> [@fruitjam](https://github.com/fruitjam), <<a href="mailto:fruitjam@gmail.com">fruitjam@gmail.com</a>>                                                                                                                                                               |
| Ubuntu           | 18.04                                | Raffael Meyer <br/> [@barredterra](https://github.com/barredterra), <<a href="mailto:raffael@alyf.de">raffael@alyf.de</a>>                                                                                                                                                                  |
| Manjaro Linux    | 20.1                                 | Sagar Vora <br/> [@sagarvora](https://github.com/sagarvora), <<a href="mailto:sagar@resilient.tech">sagar@resilient.tech</a>>                                                                                                                                                               |
| Linux Mint       | 20                                   | Walstan Baptista <br/> [@walstanb](https://github.com/walstanb), <<a href="mailto:walstan@resilient.tech">walstan@resilient.tech</a>>                                                                                                                                                       |
| Ubuntu           | 16.04.6                              | Mathieu BRUNOT <br/> [@madmath03](https://github.com/madmath03), <<a href="mailto:mathieu.brunot@monogramm.io">mathieu.brunot@monogramm.io</a>>                                                                                                                                             |
| Debian           | 9.9                                  | Bob. Followed the Python 3 path. Used Mariadb 10.3 from its origin to avoid dependency conflicts (ssllib), see [here](https://linuxize.com/post/how-to-install-mariadb-on-debian-9/#installing-mariadb-on-debian-9-from-mariadb-repositories). The path for ln above is wrong I think.<br/> |
| Debian           | 10.3                                 | X1123 <br /> [@x1123](https://github.com/x1123)                                                                                                                                                                                                                                             |
| Ubuntu           | 19.10                                | Klaus Kappel <br/> python3 path, had to set root password for mariadb.                                                                                                                                                                                                                      |
| Ubuntu - Lubuntu | 18.04                                | Hanz Tura <br/> [@hanztura](https://github.com/hanztura), <<a href="mailto:hanz@xofytech.com">hanz@xofytech.com</a>>                                                                                                                                                                        |
| CentOS 8         | CentOS Linux release 8.1.1911 (Core) | Nilesh [@nileshgr](https://github.com/nileshgr)                                                                                                                                                                                                                                             |
| Eelementary OS   | 5.1 Hera                             | x1123 [@x1123](https://github.com/x1123)<br /> python3 erpnext version-12 and I suggesting to add option command >> pip --install frappe-bench - for production server as suggested. without -e                                                                                             |
| Ubuntu           | 20.04                                | Tom <br/> Hyper-V 2012 VM, python3, mariadb 10.5 from mariadb.org (https://computingforgeeks.com/how-to-install-mariadb-on-ubuntu-focal-fossa/)</a>>                                                                                                                                        |
| Ubuntu           | 20.04                                | Adam Tang [@adamtang79](https://github.com/adamtang79)<br/>mysql_secure_installation without sudo will raise Access denied for user root@localhost                                                                                                                                          |
