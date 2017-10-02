> From Zero to Hero - [Achilles Rasquinha](https://github.com/achillesrasquinha) <<a href="mailto:achilles@frappe.io">achilles@frappe.io</a>>

<p align="justify">
To the best of my knowledge, this will be the only page you'd ever require to install <a href="https://github.com/frappe/frappe">frappé</a> right from scratch. This script also believes to be a foolproof setup to have <a href="https://github.com/frappe/frappe">frappé</a> onto your system. <b>In case if you run into some problems, feel free to raise an issue <a href="https://github.com/frappe/frappe/issues">here</a></b> with the tag <code>frappe-install</code>.
</p>
<p align="justify">
<b>NOTE:</b> To see if your Mac OS X version has been tested for the following script, check <a href="#tried-and-tested">here</a>. You're free to revise this page in order to add your Mac OS X version if you're successful with this script too (<em>psst</em>, helps others).
</p>

### Installation

First, open your Terminal (Finder > Go (Menu Bar) > Utilities > Terminal)

### TL;DR
```console
$ curl -sL bit.do/get-bench | python
```

### Brewing

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
You should then see - <b>Your system is ready to brew!</b> on your terminal screen. Fix the warnings and errors, if not.
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

### Getting <a href="https://github.com/frappe/frappe">Frappé</a> onto your system
<p align="justify">
Before going further, here's something you need to know. <a href="https://github.com/frappe/frappe">Frappé</a> is not just a web framework as a whole but also an app itself.

#### Q. Wait, what's an app?
<p align="justify">
You can think of an app in the <a href="https://github.com/frappe/frappe">Frappé</a> jargon as a collection of mutable definitions and custom functionalities for a said use-case (basically, a codebase). You then install such apps on sites (which consists of one database at a domain, files, etc.) that acts as the view layer to your app (just like any other website).
</p>

#### Q. Apps? Sites? Why would you do such a thing?
<p align="justify">
<b>Multi-tenancy</b>. <a href="https://github.com/frappe/frappe">Frappé</a> was built with an intention for you to reuse a codebase, definitions, functions, views, etc. Both, apps and sites are contained within what we call as - <em>drum rolls</em> - <b>the Bench!</b>
</p>

<p align="center">
    <img src="https://i.imgur.com/dZBThmp.png" height="150"/>
</p>

<p align="justify">
You then manage your apps and sites within your Bench. To know more, click <a href="https://www.youtube.com/watch?v=eCAMPcl7NKc&feature=youtu.be&t=32s">here</a> to completely know the architecture from the author of <a href="https://github.com/frappe/frappe">frappé</a>, <a href="https://github.com/rmehta">Rushabh Mehta</a> himself.
</p>

#### Q. Apps? Sites? And now Bench?
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

To create a new bench, simply use the `bench init` command as follows:
```console
$ bench init $MY_BENCH_NAME
```
e.g.
```console
$ bench init frappe-bench
```

### Tried and Tested
<p align="justify">
<b>NOTE:</b> If you're attempting to revise this page after successfully installing and running frappé, kindly add the required details in the following format only.
</p>

| Name         | Version | By
|--------------|---------|---
| El Capitan   | 10.11.6 | Achilles Rasquinha <br/> [@achillesrasquinha](https://github.com/achillesrasquinha), achillesrasquinha@gmail.com