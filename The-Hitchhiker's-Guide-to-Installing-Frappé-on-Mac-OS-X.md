> From Zero to Hero - [Achilles Rasquinha](https://github.com/achillesrasquinha) <<a href="mailto:achilles@frappe.io">achilles@frappe.io</a>>

<p align="justify">
To the best of my knowledge, this will be the only page you'd ever require to install <a href="https://github.com/frappe/frappe">frappé</a> right from scratch. This script also believes to be a foolproof setup to have <a href="https://github.com/frappe/frappe">frappé</a> onto your system. <b>In case if you run into some problems, feel free to raise an issue <a href="https://github.com/frappe/frappe/issues">here</a></b> with the title <code>[frappe-install]</code> followed by your issue. Your issue must have the following - System (OS) version, Dependency versions, Error Log.
</p>
<p align="justify">
<b>NOTE:</b> To see if your Mac OS X version has been tested for the following script, check <a href="#tried-and-tested">here</a>. You're free to revise this page in order to add your Mac OS X version if you're successful with this script too (<em>psst</em>, helps others).
</p>

### Installation

First, open your Terminal (Finder > Go (Menu Bar) > Utilities > Terminal)

#### TL;DR
```console
$ curl -sL bit.do/get-bench | python
```

#### Brewing

* Install [Homebrew](https://brew.sh/) - Mac OS X's package manager <br/> (Requires [Ruby](https://www.ruby-lang.org/en/downloads/) installed. To our luck, Ruby comes packaged with most Mac OS X systems)
> *On OS X El Capitan, Yosemite, Mavericks, and macOS Sierra, Ruby 2.0 is included. OS X Mountain Lion, Lion, and Snow Leopard ship with Ruby 1.8.7*
>
> Ruby Lang [Documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)

(Type `ruby --version` to check whether Ruby is available on your system)

```console
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

* Ensure your `$PATH` variable points to **Homebrew** (installed within `/usr/local/bin`)
```console
$ echo "export PATH=/usr/local/bin:/usr/local/sbin:$PATH" >> ~/.bash_profile
```

* Check whether **Homebrew** has been installed correctly
```console
$ brew doctor
```

<p align="justify">
You should then see - <b>Your system is ready to brew!</b> on your terminal screen. Fix the warnings and errors mentioned, if not.
</p>

<p align="justify">
<a href="https://github.com/frappe/frappe">Frappé</a> requires Python 2.7 installed. To our luck, Python comes shipped with most Mac OS X systems. However...
</p>

> *"The version of Python that ships with OS X is great for learning, but it’s not good for development. The version shipped with OS X may be out of date from the official current Python release, which is considered the stable production version."*
> 
> [Kenneth Reitz](https://www.kennethreitz.org/), [The Hitchhiker's Guide to Python](http://docs.python-guide.org/en/latest/starting/install/osx/)

* To install Python 2.7 on your Mac OS using `brew`, simply:
```console
$ brew install python
```

* Check whether **Python 2.7** has been installed correctly
```console
$ python --version
```
<p align="justify">
You should then see <code>Python 2.7.X</code> on your terminal screen. <b>Homebrew</b>'s Python comes with <a href="https://pip.pypa.io"><code>pip</code></a> (<em>Homebrew for Python</em>) out of the box for you.
</p>

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

![](https://i.imgur.com/QwNrzPo.png)

<p align="justify">
To know more about <b>the Bench</b>, check out <a href="https://www.youtube.com/watch?v=GVWrKuj-EAc&feature=youtu.be&t=41s">this</a> talk from the author of <a href="https://github.com/frappe/bench">bench</a> (<a href="https://github.com/pdvyas">Pratik Vyas</a>).
</p>

Go ahead and install <a href="https://git-scm.com"><code>git</code></a>
```console
$ brew install git
```

and install Bench using <a href="https://pip.pypa.io"><code>pip</code></a>
```console
$ pip install frappe-bench
```

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

Now, type [http://localhost:8000](http://localhost:8000) on your favourite browser. Login with username as - *Administrator* and your newly created password. You should then see something like this:

![](http://g.recordit.co/tuC70uxw4V.gif)

Voilà!

#### Fetching Frappé Apps
<p align="justify">
<a href="https://erpnext.org">ERPNext</a> happens to be two things - a Frappé App and <a href="https://opensource.com/resources/top-4-open-source-erp-systems">the world's best 100% Open Source ERP</a>. You can have <a href="https://github.com/frappe/erpnext">erpnext</a> fetched and stored within your bench using the following command:

```console
$ bench get-app <APP_REMOTE_URL|VALID_FRAPPE_APP>
```
e.g.
```console
$ bench get-app erpnext
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
$ bench --site foo.bar install-app erpnext
```

#### Site based multi-tenancy
<p align="justify">
Frappé lets you create multiple sites, in a single instance. Use the text-editor of your choice (I'm using nano here) and add an entry of the site you just created into the <code>/etc/hosts</code> file. 
</p>

```console
$ sudo nano /etc/hosts
```
Add the following line and save the file
```console
$ 127.0.0.1	foo.bar
```

#### You're all set!
<p align="justify">
Now you can simply access the site you just created using the link <a href="http://foo.bar:8000">foo.bar:8000</a>  
</p>

#### Tried and Tested
<p align="justify">
<b>NOTE:</b> If you're attempting to revise this page after successfully installing and running frappé, kindly add the required details in the following format only.
</p>

| Name         | Version | By
|--------------|---------|---
| macOS Sierra | 10.12.5 | Achilles Rasquinha <br/> [@achillesrasquinha](https://github.com/achillesrasquinha), <<a href="mailto:achilles@frappe.io">achilles@frappe.io</a>>
| macOS Sierra | 10.12.6 | Prateeksha Singh <br/> [@pratu16x7](https://github.com/pratu16x7), <<a href="mailto:prateeksha@frappe.io">prateeksha@frappe.io</a>>