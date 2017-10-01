> From Zero to Hero - [Achilles Rasquinha](https://github.com/achillesrasquinha)

<p align="justify">
To the best of my knowledge, this will be the only page you'd ever require to install <a href="https://github.com/frappe/frappe">frappé</a> right from scratch. This script also believes to be a foolproof setup to have <a href="https://github.com/frappe/frappe">frappé</a> onto your system. <b>In case if you run into some problems, feel free to raise an issue <a href="https://github.com/frappe/frappe/issues">here</a></b>.
</p>
<p align="justify">
<b>NOTE:</b> To see if your Mac OS X version has been tested for the following script, check <a href="#tried-and-tested">here</a>. You're free to revise this page in order to add your Mac OS X version if you're successful with this script too (<em>psst</em>, helps others).
</p>

### Installation

First, open your Terminal (Finder > Go (Menu Bar) > Utilities > Terminal)

#### Brewing

* Install [Homebrew](https://brew.sh/) - Mac OS X's package manager <br/> (Requires [Ruby](https://www.ruby-lang.org/en/downloads/) installed. To our luck, Ruby comes packaged with most Mac OS X systems)
> *On OS X El Capitan, Yosemite, Mavericks, and macOS Sierra, Ruby 2.0 is included. OS X Mountain Lion, Lion, and Snow Leopard ship with Ruby 1.8.7* - Ruby Lang [Documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)

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

You should then see - **Your system is ready to brew!** on your terminal screen. Fix the warnings and errors, if not.

<p align="justify">
Frappé requires Python 2.7 installed. To our luck, Python comes shipped with most Mac OS X systems. However
</p>

> *"The version of Python that ships with OS X is great for learning, but it’s not good for development. The version shipped with OS X may be out of date from the official current Python release, which is considered the stable production version."* - [Kenneth Reitz](https://www.kennethreitz.org/), [The Hitchhiker's Guide to Python](http://docs.python-guide.org/en/latest/starting/install/osx/)

* To install Python 2.7 on your Mac OS using `brew`, simply:
```console
$ brew install python
```

* Check whether **Python 2.7** has been installed correctly
```console
$ python --version
```
<p align="justify">
You should then see <code>Python 2.7.X</code> on your terminal screen. <b>Homebrew</b> installs <a href="https://pip.pypa.io"><code>pip</code></a> (<em>Homebrew for Python</em>) for you already.
</p>

### Tried and Tested
<p align="justify">
<b>NOTE:</b> If you're attempting to revise this page after successfully installing and running frappé, kindly add the required details in the following format only.
</p>

| Name         | Version | By
|--------------|---------|---
| El Capitan   | 10.11.6 | Achilles Rasquinha <br/> [@achillesrasquinha](https://github.com/achillesrasquinha), achillesrasquinha@gmail.com