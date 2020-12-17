Installation on Mac has become a lot more stable since the PPC days, mostly due to the increased stability of the underlying platforms. Usually takes an hour to get it right:

#### Install Xcode Select

Pre-requisite to start developing on the Mac

```
xcode-select --install
```

#### Install Homebrew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Also install `zsh` for fancy fonts on the terminal

```
brew install zsh
```

(restart terminal)

#### Python

Install Python

```
brew install python
```

Set it in path (also add it in `~/.zshrc` so that it is executed every time you open the terminal):

```
export PATH="/usr/local/opt/python/libexec/bin:$PATH" (in ~/.zshrc)
```

#### Install Pre requisites

```
brew install git node redis mariadb postgres
brew cask install Caskroom/cask/wkhtmltopdf
pip install virtualenvwrapper
npm install -g yarn
```

Start MariaDB

```
brew services start mariadb
```

To set mariadb root password, first login as your user name (no password required)

```
mysql -u USERNAME
```

Set the root password

```
set password for 'root'@'localhost' = password('NEWPASS');
flush privileges;
```

#### Install Bench

Create a folder for frappe development

```
cd ~
mkdir frappe
cd frappe
```

```
git clone https://github.com/frappe/bench bench-repo
pip install -e bench-repo
```

Create your first bench

```
bench init frappe-bench
```

