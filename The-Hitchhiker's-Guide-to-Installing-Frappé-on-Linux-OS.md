> From Zero to Hero

> [Achilles Rasquinha](https://github.com/achillesrasquinha) <[achilles@frappe.io](mailto:achilles@frappe.io)>, [Ameya Shenoy](https://github.com/codingCoffee) <[ameya@frappe.io](mailto:ameya@frappe.io)>

To the best of our knowledge, this will be the only page you'd ever require to install [frappé](https://github.com/frappe/frappe) right from scratch. This script also believes to be a foolproof setup to have [frappé](https://github.com/frappe/frappe) onto your system. **In case if you run into some problems, feel free to raise an issue [here](https://github.com/frappe/frappe/issues)** with the title `[frappe-install]` followed by your issue. Your issue must have the following - System (OS) version, Dependency versions, Error Log.

**NOTE:** To see if your Linux OS distribution has been tested for the following script, check [here](#tried-and-tested). You're free to revise this page in order to add your Linux OS distribution if you're successful with this script too (_psst_, helps others).

Note that the method described here will install Frappe's developer branch. If you want the stable production branch, follow the [Easy Install](https://github.com/frappe/bench#easy-install) method.


#### Getting [Frappé](https://github.com/frappe/frappe) onto your system

Before going further, here's something you need to know. [Frappé](https://github.com/frappe/frappe) is not just a web framework as a whole but also an app itself. ##### Q. Wait, what's an app?

You can think of an app in the [Frappé](https://github.com/frappe/frappe) jargon as a collection of mutable definitions and custom functionalities for a said use-case (basically, a codebase). You then install such apps on sites (which consists of one database at a domain, files, etc.) that acts as the view layer to your app (just like any other website).

##### Q. Apps? Sites? Why would you do such a thing?

**Multi-tenancy**. [Frappé](https://github.com/frappe/frappe) was built with an intention for you to reuse a codebase, definitions, functions, views, etc. Both, apps and sites are contained within what we call as - _drum rolls_ - **the Bench!**

<p align="center">
    <img src="https://i.imgur.com/dZBThmp.png" height="150" alt="Bench: sites and apps"/>
</p>

You then manage your apps and sites within your Bench. To know more, click [here](https://www.youtube.com/watch?v=eCAMPcl7NKc&feature=youtu.be&t=32s) to completely know the architecture from the author of [frappé](https://github.com/frappe/frappe), [Rushabh Mehta](https://github.com/rmehta) himself.

##### Q. Apps? Sites? And now Bench? 

Yes, the Bench! You can think of the bench as the guardian for both, your apps and sites. Bench is the heart and soul of apps and sites built using the [frappé](https://github.com/frappe/frappe) framework. You store, update, manage and mutate apps within your bench. Not just that > [`bench`](https://github.com/frappe/bench) is to frappé, what `apt-get` is to Debian-based Linux OS :wink:

We provide you the [`bench`](https://github.com/frappe/bench) command-line tool for you to create Benches, Apps and Sites. For installing apps built on Frappé, we use [`git`](https://git-scm.com) as our Source Control Manager (SCM) to have them fetched from remote repositories.
![](https://i.imgur.com/QwNrzPo.png)

To get to know more about **Bench**, check out [this](https://www.youtube.com/watch?v=GVWrKuj-EAc&feature=youtu.be&t=41s) talk from the author of [bench](https://github.com/frappe/bench) ([Pratik Vyas](https://github.com/pdvyas)).

### Installation

First, open your Terminal (`Ctrl` + `Alt` + `T`)

### Dependencies

* Install [`git`](https://git-scm.com)

  **Debian/Ubuntu**

```console
$ sudo apt-get install git
```

* Check whether **git** has been installed correctly

```console
$ git --version
```

You should then see `git version X.Y.Z` on your terminal screen.

[Frappé](https://github.com/frappe/frappe) requires Python 2.7 installed. To our luck, Python comes shipped with most Linux OS distributions. However, we might require the `python-dev` package installed for using Python's C API.

* To install Python 2.7.X `dev` package on your Linux OS, simply:

  **Debian/Ubuntu**

```console
$ sudo apt-get install python-dev
```

* Install `setuptools` and `pip` (Python's Package Manager):

```console
$ sudo apt-get install python-setuptools python-pip
```

[Frappé](https://github.com/frappe/frappe) uses [MariaDB](https://mariadb.org) (for [RDBMS](https://en.wikipedia.org/wiki/Relational_database_management_system)) as its database engine, [Redis](https://redis.io) for caching and as a message broker and [Node.js](https://nodejs.org) for everything JavaScript. Go ahead and install 'em all.
**Debian/Ubuntu**

* To install MariaDB 10.3 `stable` package on your Linux OS, simply:

```console
$ sudo apt-get install software-properties-common
$ sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
$ sudo add-apt-repository 'deb [arch=amd64,i386,ppc64el] http://ftp.ubuntu-tw.org/mirror/mariadb/repo/10.3/ubuntu xenial main'

$ sudo apt-get update
$ sudo apt-get install mariadb-server-10.3
```

During this installation you'll be prompted to set the MySQL root password. If you are not prompted for the same, you'll have to initialize the MySQL server setup yourself after the above command completes. You can initialize the MySQL server setup by executing the following command `mysql_secure_installation`. **Remember**: only run it if you're not prompted the password during setup.

It is really important that you remember this password, since it'll be needed later on! 
Test whether the installation has worked with `mysql -u root -p -h localhost`. You should be prompted for the mysql root password you have provided during the installation. Get back out of the mysql console by typing `\q`
 
Next you'll need the MySQL database development files

```console
$ sudo apt-get install libmysqlclient-dev
```

You also need to edit the mariadb configuration (although the guide in README doesn't mention this, you'll face an error message asking you to do exactly this if you follow the README. So you might as well go ahead and do this)

```console
$ sudo nano /etc/mysql/my.cnf
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

(Now press (Ctrl-X) to exit!)
Finally restart the mysql server and you'll be good to go!
```console
$ sudo service mysql restart
```

* To install Redis on your Linux OS, simply:
```console
$ sudo apt-get install redis-server
```

* To install Node.js 8.X package on your Linux OS, simply:
```console
$ sudo apt-get install curl
$ curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
$ sudo apt-get install -y nodejs
```

* To install yarn run
```console
$ sudo npm install -g yarn
```

#### Getting [Bench](https://github.com/frappe/bench) onto your system

Install Bench from the github repository

```console
$ git clone https://github.com/frappe/bench
$ pip install -e ./bench
```

OR directly [from pip](https://pypi.org/project/frappe-bench/):

```console
$ pip install frappe-bench
```

> Bench has been [pip](https://pip.pypa.io)ed (Click [here](https://github.com/frappe/bench/pull/490) for more details).

* Check whether **Bench** has been installed correctly
```console
$ bench --version
```
You should then see `X.Y.Z` on your terminal screen.

And there you have it! You're now ready to build something awesome using [frappé](https://github.com/frappe/frappe)

#### Bench - Quickstart
To create a new bench, simply use the `bench init` command as follows:
```console
$ bench init <MY_BENCH>
```
e.g.
```console
$ bench init frappe-bench
```

This goes ahead and creates a folder named `frappe-bench` with a whole lot of stuff inside! This might take a while (depending on your internet speed). We, at frappé love our coffee with flavour. Go get one brewed for yourself.

Once done, simply change to your bench directory:
```console
$ cd <MY_BENCH>
```
e.g.
```console
$ cd frappe-bench
```

#### What should you see?

Typing an `ls` on your terminal, you should see the following:
```console
├── 🗄️ apps               # frappé apps
├── 🗄️ config             # all configuration files (*.conf)
├── 🗄️ env                # virtual environment (an isolated python environment catering to python dependencies for frappé apps only)
├── 🗄️ logs               # all log files
├── 🗄️ node_modules       # collective node dependencies for frappé apps
├── 🗄️ sites              # frappé sites
├── 📁 package.json       # list of node dependencies
├── 📁 package-lock.json  # locking the list of node dependencies
├── 📁 patches.txt        # list of patches patched
├── 📁 Procfile           # process file (to let honcho activate a list of all processes)
```

Go ahead and start bench as follows:
```console
$ bench start
```

#### Creating Sites

**NOTE:** You might need another terminal instance to run the following commands within the path to your `MY_BENCH` directory.

```console
$ bench new-site <MY_SITE>
```
e.g.
```console
$ bench new-site foo.bar
```

You'll be then prompted to type your MySQL root password (which then goes ahead and creates a new database for your site). You'd also be prompted to create a new password for the System Administrator. A site comes with frappé installed by default. Like I mentioned

> Frappé is not just a web framework as a whole but also an app itself.

#### Site based multi-tenancy

Frappé lets you create multiple sites, in a single instance. To enable site based multi-tenancy empty the contents of the file `currentsite.txt` using the text-editor of your choice (I'm using nano here)

```console
$ bench config dns_multitenant on
$ nano sites/currentsite.txt
```

Then add an entry of the site you just created into the `/etc/hosts` file.

```console
$ sudo nano /etc/hosts
```

Add the following line and save the file
```console
$ 127.0.0.1	foo.bar
```

#### Fetching Frappé Apps

[ERPNext](https://erpnext.org) happens to be two things - a Frappé App and [the world's best 100% Open Source ERP](https://opensource.com/resources/top-4-open-source-erp-systems). You can have [erpnext](https://github.com/frappe/erpnext) fetched and stored within your bench using the following command:

```console
$ bench get-app <APP_REMOTE_URL|VALID_FRAPPE_APP>
```

e.g.

```console
$ bench get-app erpnext
```

This goes ahead and fetches the complete source code and places it within your `MY_BENCH/apps/MY_APP_NAME` folder. In this case - `frappe-bench/apps/erpnext`

#### Installing Frappé Apps onto Sites
```console
$ bench --site <MY_SITE> install-app <MY_APP_NAME>
```
e.g.
```console
$ bench --site foo.bar install-app erpnext
```

#### You're all set!

Now you can simply access the site you just created using the link [foo.bar:8000](http://foo.bar:8000)

#### Tried and Tested

**NOTE:** If you're attempting to revise this page after successfully installing and running frappé, kindly add the required details in the following format only.

| Name         | Version | By
|--------------|---------|---
| Ubuntu       | 16.04.1 | Ameya Shenoy <br/> [@codingCoffee](https://github.com/codingCoffee), <<a href="mailto:ameya@frappe.io">ameya@frappe.io</a>>
| Ubuntu       | 18.04   | Ameya Shenoy <br/> [@codingCoffee](https://github.com/codingCoffee), <<a href="mailto:ameya@frappe.io">ameya@frappe.io</a>>
| Ubuntu       | 16.04.5 | Achilles Rasquinha <br/> [@achillesrasquinha](https://git.io/achilles), <<a href="mailto:achillesrasquinha@gmail.com">achillesrasquinha@gmail.com</a>>
| Linux Mint   | 19      | Sagar Vora <br/> [@sagarvora](https://github.com/sagarvora), <<a href="mailto:sagar@resilient.tech">sagar@resilient.tech</a>>