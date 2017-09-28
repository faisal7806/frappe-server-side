> From Zero to Hero - [Achilles Rasquinha](https://github.com/achillesrasquinha)

<p align="justify">
To the best of my knowledge, this will be the only page you'd ever require to install <a href="https://github.com/frappe/frappe">frappe</a> right from scratch. This script also believes to be a foolproof setup to have <a href="https://github.com/frappe/frappe">frappe</a> onto your system. <b>In case if you run into some problems, feel free to raise an issue <a href="https://github.com/frappe/frappe/issues">here</a></b>.
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

* Check whether **Homebrew** has been installed correctly
```console
$ brew doctor
```

You should then see - **Your system is ready to brew!** on your terminal screen

### Tried and Tested
<p align="justify">
<b>NOTE:</b> If you're attempting to revise this page after successfully installing and running frappe, kindly add the required details in the following format only.
</p>

| Name         | Version | By
|--------------|---------|---
| El Capitan   | 10.11.6 | Achilles Rasquinha <br/> [@achillesrasquinha](https://github.com/achillesrasquinha), achillesrasquinha@gmail.com