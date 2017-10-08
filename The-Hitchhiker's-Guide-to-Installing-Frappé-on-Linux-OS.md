> From Zero to Hero
> 
> [Achilles Rasquinha](https://github.com/achillesrasquinha) <<a href="mailto:achilles@frappe.io">achilles@frappe.io</a>>, [Ameya Shenoy](https://github.com/codingCoffee) <<a href="mailto:ameya@frappe.io">ameya@frappe.io</a>>

<p align="justify">
To the best of my knowledge, this will be the only page you'd ever require to install <a href="https://github.com/frappe/frappe">frappé</a> right from scratch. This script also believes to be a foolproof setup to have <a href="https://github.com/frappe/frappe">frappé</a> onto your system. <b>In case if you run into some problems, feel free to raise an issue <a href="https://github.com/frappe/frappe/issues">here</a></b> with the title <code>[frappe-install]</code> followed by your issue.
</p>
<p align="justify">
<b>NOTE:</b> To see if your Linux OS distribution has been tested for the following script, check <a href="#tried-and-tested">here</a>. You're free to revise this page in order to add your Linux OS distribution if you're successful with this script too (<em>psst</em>, helps others).
</p>

#### Getting <a href="https://github.com/frappe/frappe">Frappé</a> onto your system
<p align="justify">
Before going further, here's something you need to know. <a href="https://github.com/frappe/frappe">Frappé</a> is not just a web framework as a whole but also an app itself.

##### Q. Wait, what's an app?
<p align="justify">
You can think of an app in the <a href="https://github.com/frappe/frappe">Frappé</a> jargon as a collection of mutable definitions and custom functionalities for a said use-case (basically, a codebase). You then install such apps on sites (which consists of one database at a domain, files, etc.) that acts as the view layer to your app (just like any other website).
</p>

##### Q. Apps? Sites? Why would you do such a thing?
<p align="justify">
<b>Multi-tenancy</b>. <a href="https://github.com/frappe/frappe">Frappé</a> was built with an intention for you to reuse a codebase, definitions, functions, views, etc. Both, apps and sites are contained within what we call as - <em>drum rolls</em> - <b>the Bench!</b>
</p>

<p align="center">
    <img src="https://i.imgur.com/dZBThmp.png" height="150"/>
</p>

<p align="justify">
You then manage your apps and sites within your Bench. To know more, click <a href="https://www.youtube.com/watch?v=eCAMPcl7NKc&feature=youtu.be&t=32s">here</a> to completely know the architecture from the author of <a href="https://github.com/frappe/frappe">frappé</a>, <a href="https://github.com/rmehta">Rushabh Mehta</a> himself.
</p>

##### Q. Apps? Sites? And now Bench?
Yes, the Bench! You can think of the bench as the guardian for both, your apps and sites. Bench is the heart and soul of apps and sites built using the <a href="https://github.com/frappe/frappe">frappé</a> framework. You store, update, manage and mutate apps within your bench. Not just that
> [`bench`](https://github.com/frappe/bench) is to frappé, what `apt-get` is to Debian-based Linux OS :wink:

<p align="justify">
We provide you the <a href="https://github.com/frappe/bench"><code>bench</code></a> command-line tool for you to create Benches, Apps and Sites. For installing apps built on Frappé, we use <a href="https://git-scm.com"><code>git</code></a> as our Source Control Manager (SCM) to have them fetched from remote repositories.
</p>

<p align="justify">
To know more about <b>the Bench</b>, check out <a href="https://www.youtube.com/watch?v=GVWrKuj-EAc&feature=youtu.be&t=41s">this</a> talk from the author of <a href="https://github.com/frappe/bench">bench</a> (<a href="https://github.com/pdvyas">Pratik Vyas</a>).
</p>

### Installation

First, open your Terminal (`Ctrl` + `Alt` + `T`)

### Dependencies

* Install [`git`](https://git-scm.com)

**Debian**
```console
$ sudo apt-get install git
```

* Check whether **git** has been installed correctly
```console
$ git --version
```

<p align="justify">
You should then see <code>git version X.Y.Z</code> on your terminal screen.
</p>

<p align="justify">
<a href="https://github.com/frappe/frappe">Frappé</a> requires Python 2.7 installed. To our luck, Python comes shipped with most Linux OS distributions. However, we might require the `python-dev` package installed for using Python's C API.
</p>

* To install Python 2.7 `dev` package on your Linux OS, simply:

**Debian**
```console
$ sudo apt-get install python-dev
```

* Install `pip` (Python's Package Manager):
```console
$ wget -O - https://bootstrap.pypa.io/get-pip.py | python
```


<p align="justify">
<a href="https://github.com/frappe/frappe">Frappé</a> uses <a href="https://mariadb.org">MariaDB</a> (for <a href="https://en.wikipedia.org/wiki/Relational_database_management_system">RDBMS</a>) as its database engine, <a href="https://redis.io">Redis</a> for caching and as a message broker and <a href="https://nodejs.org">Node.js</a> for everything JavaScript. Go ahead and install 'em all.
</p>

```console
$ brew install mariadb redis node
```

<p align="justify">
<b>Homebrew</b>'s Node.js comes with <a href="https://www.npmjs.com"><code>npm</code></a> (<em>Homebrew for Node.js</em>) installed for you.
</p>

#### Getting <a href="https://github.com/frappe/frappe">Frappé</a> onto your system
<p align="justify">
Before going further, here's something you need to know. <a href="https://github.com/frappe/frappe">Frappé</a> is not just a web framework as a whole but also an app itself.

##### Q. Wait, what's an app?
<p align="justify">
You can think of an app in the <a href="https://github.com/frappe/frappe">Frappé</a> jargon as a collection of mutable definitions and custom functionalities for a said use-case (basically, a codebase). You then install such apps on sites (which consists of one database at a domain, files, etc.) that acts as the view layer to your app (just like any other website).
</p>

##### Q. Apps? Sites? Why would you do such a thing?
<p align="justify">
<b>Multi-tenancy</b>. <a href="https://github.com/frappe/frappe">Frappé</a> was built with an intention for you to reuse a codebase, definitions, functions, views, etc. Both, apps and sites are contained within what we call as - <em>drum rolls</em> - <b>the Bench!</b>
</p>

<p align="center">
    <img src="https://i.imgur.com/dZBThmp.png" height="150"/>
</p>

<p align="justify">
You then manage your apps and sites within your Bench. To know more, click <a href="https://www.youtube.com/watch?v=eCAMPcl7NKc&feature=youtu.be&t=32s">here</a> to completely know the architecture from the author of <a href="https://github.com/frappe/frappe">frappé</a>, <a href="https://github.com/rmehta">Rushabh Mehta</a> himself.
</p>

##### Q. Apps? Sites? And now Bench?
Yes, the Bench! You can think of the bench as the guardian for both, your apps and sites. Bench is the heart and soul of apps and sites built using the <a href="https://github.com/frappe/frappe">frappé</a> framework. You store, update, manage and mutate apps within your bench. Not just that
> [`bench`](https://github.com/frappe/bench) is to frappé, what Homebrew is to Mac OS X :wink:

<p align="justify">
We provide you the <a href="https://github.com/frappe/bench"><code>bench</code></a> command-line tool for you to create Benches, Apps and Sites. For installing apps built on Frappé, we use <a href="https://git-scm.com"><code>git</code></a> as our Source Control Manager (SCM) to have them fetched from remote repositories.
</p>

<p align="justify">
To know more about <b>the Bench</b>, check out <a href="https://www.youtube.com/watch?v=GVWrKuj-EAc&feature=youtu.be&t=41s">this</a> talk from the author of <a href="https://github.com/frappe/bench">bench</a> (<a href="https://github.com/pdvyas">Pratik Vyas</a>).
</p>

Go ahead and install <a href="https://git-scm.com"><code>git</code></a>
```console
$ brew install git
```

and install Bench using <a href="https://pip.pypa.io"><code>pip</code></a>
```console
$ pip install -e git+https://github.com/frappe/bench#egg=frappe-bench
```

NOTE: We're having Bench <a href="https://pip.pypa.io"><code>pip</code></a>ed soon (Click [here](https://github.com/frappe/bench/pull/490) for more details).

* Check whether **Bench** has been installed correctly
```console
$ bench --version
```
<p align="justify">
You should then see <code>X.Y.Z</code> on your terminal screen.

<p align="justify">
And there you have it! You're now ready to build something awesome using <a href="https://github.com/frappe/frappe">frappé</a>
</p>

#### Bench - Quickstart
To create a new bench, simply use the `bench init` command as follows:
```console
$ bench init <MY_BENCH>
```
e.g.
```console
$ bench init frappe-bench
```

<p align="justify">
This goes ahead and creates a folder named <code>frappe-bench</code> with a whole lot of stuff inside! This might take a while (depending on your internet speed). We, at frappé love our coffee with flavour. Go get one brewed for yourself.
</p>

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
<p align="justify">
<b>NOTE:</b> You might need another terminal instance to run the following commands within the path to your <code>MY_BENCH</code> directory.
</p>

```console
$ bench new-site <MY_SITE>
```
e.g.
```console
$ bench new-site foo.bar
```

<p align="justify">
You'll be then prompted to type your MySQL root password (which then goes ahead and creates a new database for your site). You'd also be prompted to create a new password for the System Administrator. A site comes with frappé installed by default. Like I mentioned
</p>

> Frappé is not just a web framework as a whole but also an app itself.

#### Fetching Frappé Apps
<p align="justify">
<a href="https://erpnext.org">ERPNext</a> happens to be two things - a Frappé App and <a href="https://opensource.com/resources/top-4-open-source-erp-systems">the world's best 100% Open Source ERP</a>. You can have <a href="https://github.com/frappe/erpnext">erpnext</a> fetched and stored within your bench using the following command:

```console
$ bench get-app <MY_APP_NAME> <APP_REMOTE_URL>
```
e.g.
```console
$ bench get-app erpnext https://github.com/frappe/erpnext
```
<p align="justify">
This goes ahead and fetches the complete source code and places it within your <code>MY_BENCH/apps/MY_APP_NAME</code> folder. In this case - <code>frappe-bench/apps/erpnext</code>
</p>

#### Installing Frappé Apps onto Sites
```console
$ bench --site <MY_SITE> install-app <MY_APP_NAME>
```
e.g.
```console
$ bench install-app erpnext --site foo.bar
```

#### Tried and Tested
<p align="justify">
<b>NOTE:</b> If you're attempting to revise this page after successfully installing and running frappé, kindly add the required details in the following format only.
</p>

| Name         | Version | By
|--------------|---------|---
| Ubuntu       | 16.04.1 | Ameya Shenoy <br/> [@codingCoffee](https://github.com/codingCoffee), <<a href="mailto:ameya@frappe.io">ameya@frappe.io</a>>