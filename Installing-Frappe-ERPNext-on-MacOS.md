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
export PATH="/usr/local/opt/python/libexec/bin:$PATH"
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

Set encodings:

Edit `vim /usr/local/etc/my.cnf`

```
[mysqld]
innodb-file-format=barracuda
innodb-file-per-table=1
innodb-large-prefix=1
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

[mysql]
default-character-set = utf8mb4
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

#### Install ERPNext

```
bench get-app erpnext
```

(Debugging tips: if python libraries fail, try changing the versions of the pre-requisites in `apps/erpnext/requirements.txt`)

#### Setup `/etc/hosts`

```
Add your sites in /etc/hosts

127.0.0.1 frappe1.local frappe2.local
```

#### Create your first site

Create your first site

```
bench start
```

On a new bench

```
bench new-site frappe1.local
```
