Running Frappe on Windows is not officially supported and should be considered for development purposes only; do not attempt to run a production instance with critical data on a Windows machine. This is a brief overview, other steps may be required depending on your configuration. This installation is more difficult that installing on MacOS or Linux. 

* [Install Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
* Install Ubuntu 18.04 (tested, you can try other distributions) from the app store
* Open a command prompt and enter `bash` to stop using powershell
* [Follow these instructions once inside the bash shell](https://github.com/frappe/frappe/wiki/The-Hitchhiker%27s-Guide-to-Installing-Frappe-on-Linux)

Windows does not permit systemd to run, so you'll have to choose an alternative for staring the bench:

* Create a bash script to start mariadb and redis, following this guide https://dev.to/ironfroggy/wsl-tips-starting-linux-background-services-on-windows-login-3o98
* If you do not want to start mariadb and redis when you log into windows you can start them manually with the bash command `sudo service mysql start && sudo service redis-server start`
* A third alternative is to [alias](https://www.tecmint.com/create-alias-in-linux/) a command to `bench start`: `sudo service mysql start && sudo service redis-server start && bench start`