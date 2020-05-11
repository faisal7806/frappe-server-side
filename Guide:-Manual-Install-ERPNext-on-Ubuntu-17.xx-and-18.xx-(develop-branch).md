<h1>NOTE:</h1>
<p>1). Clean install on Ubuntu</p>
<p>2). User is bench with sudo privileges </p>
<p>3). Installed on Virtualbox Virtual machines</p>

Login to your Local User

<h2>Prerequisites</h2>

Ubuntu 17.XX or 18.XX server instance.
<pre>
<code>sudo apt update
sudo apt -y upgrade
</code>
</pre>

<h3>Install Development Tools</h3>

<p>ERPNext needs Python version 2.7 to work. Install Python 2.7.</p>
<pre>
<code>sudo apt -y install python-minimal</code>
You should be able to verify its version.
<code>python -V</code>
</pre>

Install a few more dependencies.
<pre>
<code>sudo apt -y install git build-essential python-setuptools python-dev libffi-dev libssl-dev
</code>
</pre>

<p>"Install Python's <code>pip</code> tool. Pip is the dependency for Python Pakages."</p>

<pre>
<code>wget https://bootstrap.pypa.io/get-pip.py
sudo python get-pip.py
</code>
</pre>

<p>
"Ensure that you have the latest version of " 
<code>pip</code>
" and " 
<code>setuptools</code>
"."
</p>
<pre>
<code>sudo pip install --upgrade pip setuptools
</code>
</pre>

Install Ansible using Pip. Ansible automates software provisioning, configuration management, and application deployment.

<pre><code>sudo pip install ansible
</code>
</pre>

Install <code>yarn</code> On Debian or Ubuntu Linux, you can install Yarn via our Debian package repository. You will first need to configure the repository

<pre>
<code>curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
</code>
</pre>

Then you can simply
<pre>
<code>sudo apt-get update && sudo apt-get install yarn
</code>
</pre>

<h3>Install MariaDB Server</h3>

Add the MariaDB repository into the system.
<pre>
<code>sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
sudo add-apt-repository 'deb [arch=amd64,i386,ppc64el] http://mirror.nodesdirect.com/mariadb/repo/10.2/ubuntu xenial main'
</code>
</pre>

Install MariaDB.
<pre><code>sudo apt update
sudo apt -y install mariadb-server libmysqlclient-dev</code></pre>

Provide a strong password for the MariaDB root user when asked.

The Barracuda storage engine is required for the creation of ERPNext databases, so you will need to configure MariaDB to use the Barracuda storage engine. Edit the default MariaDB configuration file <code>my.cnf</code>
<pre>
<code>sudo nano /etc/mysql/my.cnf
</code>
</pre>

Add the following lines under the <code>[mysqld]</code> line.
<pre>
<code>innodb-file-format=barracuda
innodb-file-per-table=1
innodb-large-prefix=1
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
</code>
</pre>

Also, add the following line under the <code>[mysql]</code> line.
<pre>
<code>default-character-set = utf8mb4
</code>
</pre>

Restart MariaDB and enable it to automatically start at boot time.
<pre>
<code>sudo systemctl restart mariadb
sudo systemctl enable mariadb
</code>
</pre>

Before configuring the database, you will need to secure MariaDB. You can secure it by running the <code>mysql_secure_installation</code> script.
<pre>
<code>sudo mysql_secure_installation
</code>
</pre>

<h3>Install Nginx, Node.js and Redis</h3>

Add the Nodesource repository for Node.js 8.x.
<pre>
<code>sudo curl --silent --location https://deb.nodesource.com/setup_10.x | sudo bash -
</code>
</pre>

Install Nginx, Node.js and Redis.
<pre>
<code>sudo apt -y install nginx nodejs redis-server
</code>
</pre>

Start Nginx and enable it to start at boot time.
<pre>
<code>sudo systemctl start nginx
sudo systemctl enable nginx
</code>
</pre>

Start Redis and enable it to start at boot time.
<pre>
<code>sudo systemctl start redis-server
sudo systemctl enable redis-server
</code>
</pre>

<h3>Install PDF Converter</h3>

The wkhtmltopdf program is a command line tool that converts HTML into PDF using the QT Webkit rendering engine. Install the required dependencies.
<pre>
<code>sudo apt -y install libxrender1 libxext6 xfonts-75dpi xfonts-base
</code>
</pre>

Download the latest version of wkhtmltopdf.
<pre>
<code>wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
</code>
</pre>

Extract the archive.
<pre>
<code>sudo tar -xf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz -C /opt
</code>
</pre>

The above command will extract the archive to /opt/wkhtmltox. Create a softlink so that wkhtmltopdf and wkhtmltoimage can be executed globally as a command.
<pre>
<code>sudo ln -s /opt/wkhtmltox/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
sudo ln -s /opt/wkhtmltox/bin/wkhtmltoimage /usr/bin/wkhtmltoimage
</code>
</pre>

You can now run wkhtmltopdf -V to check if it is working, you will see this.
<pre>
<code>wkhtmltopdf -V
Result wkhtmltopdf 0.12.4 (with patched qt)
</code>
</pre>

At this point, we have all the required dependencies installed. You can now proceed to install Bench.

<h3>Install Bench</h3>
Bench is a command line utility provided by Frappe to install and manage the ERPNext application on a Unix-based system for both development and production purposes. Bench can also create and manage Nginx and supervisor configurations.

Create a new user to run Bench processes in the isolated environment.

<pre>
<code>sudo adduser bench --home /opt/bench
</code>
</pre>

Provide sudo permissions to the bench user.
<pre>
<code>sudo usermod -aG sudo bench
</code>
</pre>

Login as the newly created bench user.
<pre>
<code>sudo su - bench
</code>
</pre>

Clone the Bench repository in /opt/bench.
<pre>
<code>cd /opt/bench
git clone https://github.com/frappe/bench bench-repo
</code>
</pre>

Install Bench using pip.
<pre>
<code>sudo pip install -e bench-repo
</code>
</pre>

Once Bench is installed, proceed further to install ERPNext using Bench.


<h3>Install ERPNext using Bench</h3>

Initialize a bench directory with frappe framework installed. To keep everything tidy, we will work under the /opt/bench directory. Bench will also setup regular backups and auto updates once a day.
<pre>
<code>cd /opt/bench
bench init erpnext && cd erpnext
</code>
</pre>

Create a new Frappe site.
<pre>
<code>bench new-site erp.example.com
</code>
</pre>

The above command will prompt you for the MySQL root password. Provide the password which you have set for the MySQL root user earlier. It will also ask you to set a new password for the administrator account. You will need this password later to log into the administrator dashboard.

Download ERPNext installation files from the remote git repository using Bench.
<pre>
<code>bench get-app erpnext https://github.com/frappe/erpnext
</code>
</pre>

Install ERPNext on your newly created site.
<pre>
<code>bench --site erp.example.com install-app erpnext
</code>
</pre>

You can start the application immediately to check if the application installed successfully.
<pre>
<code>bench start
</code>
</pre>

However, you should stop the execution and proceed further to set up the application for production use.

<h3>Database Login Issues</h3>
In some cases Database may not login, to rectify the issue Please Follow below steps

<pre>
<code>sudo vim /etc/mysql/my.cnf
</code>
</pre>

Add the following lines at the end:
<pre>
<code>[mysqld]

skip-grant-tables
</code>
</pre>

Then Restart the service
<pre>
<code>sudo service mysql restart
</code>
</pre>

Login to Mysql & follow the command
<pre>
<code>mysql -u root

use mysql

select * from mysql where user = 'root'; - Look at the top to determine whether the password column is called password or authentication_string

UPDATE mysql.user set *password_field from above* = PASSWORD('your_new_password') where user = 'root' and host = 'localhost'; - Use the proper password column from above

SELECT User, Host, plugin FROM user;
</code>
</pre>

If Plugin is not mysql_native_password, then set the plugin by the below command
<pre><code>UPDATE user SET plugin='mysql_native_password' WHERE User='root';
FLUSH PRIVILEGES;
exit;
</code></pre>

Remove the skip-grant-tables from /etc/mysql/my.cnf, restart the service & it's Done

<h3>Setup Supervisor & Nginx for Production</h3>

By default, the ERPNext application listens on port 8000, not the standard HTTP port 80. Also, running the built in web server for production use is not recommended as we will be exposing the server to the world. You should use a production web server as a reverse proxy such as Apache or Nginx. We will use Nginx as a reverse proxy as it can be automatically configured using Bench. Bench can automatically generate and install the configuration according to the ERPNext setup.

Although we can start the application using the 'bench start' command, the execution of ERPNext will stop as soon as you close the terminal. To overcome this issue, you should use Supervisor, which is very helpful in running the application continuously in a production environment. Supervisor is a process control system that enables you to monitor and control a number of processes on Linux operating systems. Once Supervisor is configured, it will automatically start the application at boot time as well as on failures. Bench can automatically configure Supervisor for the ERPNext application.

Install Supervisor.
<pre><code>sudo apt -y install supervisor</code></pre>

Start Supervisor and enable it to automatically start at boot time.
<pre><code>sudo systemctl start supervisor
sudo systemctl enable supervisor
</code></pre>

Setup Bench for production use.
<pre><code>sudo bench setup production bench
</code></pre>

The above command may prompt you before replacing the existing Supervisor default configuration file with a new one. Choose y to proceed. Bench adds a number of processes to the Supervisor configuration file. The above command will also ask you if you wish to replace the current Nginx configuration with a new one. Enter y to proceed. Once Bench has finished installing the configuration, provide other users to execute the files in your home directory of the Bench user.
<pre><code>chmod o+x /opt/bench/
</code></pre>

You can now access the site on http://erp.example.com.

You can check the status of the processes by running.
<pre><code>sudo supervisorctl status all</code></pre>

You should see the following output.
<pre><code>sudo supervisorctl status all
erpnext-redis:erpnext-redis-cache                 RUNNING   pid 13852, uptime 0:00:54
erpnext-redis:erpnext-redis-queue                 RUNNING   pid 13851, uptime 0:00:54
erpnext-redis:erpnext-redis-socketio              RUNNING   pid 13853, uptime 0:00:54
erpnext-web:erpnext-frappe-web                    RUNNING   pid 13856, uptime 0:00:54
erpnext-web:erpnext-node-socketio                 RUNNING   pid 13855, uptime 0:00:54
erpnext-workers:erpnext-frappe-default-worker-0   RUNNING   pid 13862, uptime 0:00:54
erpnext-workers:erpnext-frappe-long-worker-0      RUNNING   pid 13870, uptime 0:00:54
erpnext-workers:erpnext-frappe-schedule           RUNNING   pid 13869, uptime 0:00:54
erpnext-workers:erpnext-frappe-short-worker-0     RUNNING   pid 13875, uptime 0:00:54
</code></pre>

To stop and Start all of the ERPNext processes.
<pre><code>sudo supervisorctl stop all
sudo supervisorctl start all
</code></pre>
