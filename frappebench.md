# FRAPPE FRAMEWORK TUTORIAL

## WHAT TOOLS DO WE NEED TO CREATE AN APP? 
1. Coding Language: Python, Javascript,
2. Database: MariaDB and SQL databases
3. Version Control: Git
4. User Interface: HTML
5. Jinja Templating: used to generate any markup as well as source code
6. Javascript/JQuery: JQuery is library in Javascript. It is used to provide an easy way to use javascript on your website to make it more attractive.

## STEPS OF INSTALLATION 
Ensure that you are on macbook/linux OS.

### SERVER SETUP <BR>
Login to the server as root user.

#### To Update & upgrade server packages
sudo apt-get update -y <BR>
sudo apt-get upgrade -y

#### Create new user
$sudo adduser [frappe-user] <BR>
$usermod -aG sudo [frappe-user]   // The command is used to grant administrative privileges to the specified user, allowing them to run commands with elevated permissions by accessing sudo file. <br>

*If permission to access sudoers file is denied*
##### To give access/permission to newly built user:
1. Open new terminal with root user (or user which has access of sudoers file) and use 'visudo' command to edit sudoers file
2. Once you are inside sudoers file add:<br>
[frappe-username] ALL=(ALL:ALL) ALL
3. Save changes and come back to sudo user terminal and you are ready to continue.

NEXT COMMNDS:<br>
su [frappe-user] ///switching user <BR>
cd /home/[frappe-user]/      //changing directory 

### INSTALL REQUIRED PACKAGES
#### To install git
sudo apt-get install git    //apt-get is packager manager used.

#### Install Python 
sudo apt-get install python3-dev python3.10-dev python3-setuptools python3-pip python3-distutils

#### Install Python Virtual Environment
sudo apt-get install python3.10-venv   //This command will download and install the Python 3.10 virtual environment package, which allows you to create isolated Python environments to manage project dependencies.The sudo command allows regular users to perform tasks that are typically reserved for the system administrator (root user) 

#### Install Software Properties Common (for repository management) 
 sudo apt-get install software-properties-common   //It is used to install the "software-properties-common" package on Debian-based Linux distributions, such as Ubuntu. This package contains various utilities that make it easier to manage software repositories and perform related tasks.

#### Install MariaDB (MySQL server) 
 sudo apt install mariadb-server mariadb-client

#### Install Redis Server 
 sudo apt-get install redis-server
 
### CONFIGURE MYSQL SERVER 
 $ sudo mysql_secure_installation
 1. Enter current password for root: (Enter your SSH root user password)
 2. Switch to unix_socket authentication [Y/n]: Y
 3. Change the root password? [Y/n]: Y<br>
    *NEVER MISS THIS STEP AND REMEMBER THE SET PASSWORD AS YOU WILL BE ASKED LATER.*
 5. It will ask you to set new MySQL root password at this step. This can be different from the SSH root user password.
 6. Remove anonymous users? [Y/n] Y
 7. Disallow root login remotely? [Y/n]: N
 8. This is set as N because we might want to access the database from a remote server for using business analytics software like Metabase / PowerBI / Tableau, etc.
 9. Remove test database and access to it? [Y/n]: Y
 10. Reload privilege tables now? [Y/n]: Y

#### Edit the MySQL default config file
sudo vim /etc/mysql/my.cnf<br>
*if VIM file is not installed then:*
$sudo apt install vim       //Vim is an editor to create or edit a text file
<br>
Add the below code block at the bottom of the file;

[mysqld]
character-set-client-handshake = FALSE <br>
character-set-server = utf8mb4 <br>
collation-server = utf8mb4_unicode_ci

[mysql]
default-character-set = utf8mb4

#### Restarting MYSQL Server<br>
sudo service mysql restart

### INSTALL CURL, Node, NPM and Yarn<br>

#### Install CURL <BR>
sudo apt install curl        //Curl" is a command-line tool and a library used in various programming languages to transfer data to or from a server

#### Install Node <BR>
//open-source, server-side runtime environment built on Chrome's V8 JavaScript engine <br>
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash<BR>
source ~/.profile <BR>
nvm install 16.15.0

#### Install NPM <BR>
sudo apt-get install npm        //"NPM" stands for "Node Package Manager".It is used to install, manage, and share reusable JavaScript code packages.

#### Install Yarn <BR>
sudo npm install -g yarn       // Like NPM, Yarn is used to manage JavaScript packages.

### FRAPPE BENCH

#### Install Frappe Bench
sudo pip3 install frappe-bench

####  Initialize Frappe Bench
bench init --frappe-branch version-14 frappe-bench

####  Go to Frappe Bench directory
cd frappe-bench/

####  Change user directory permissions
chmod -R o+rx /home/[frappe-user]/             //o+rx adds read and execute permissions for others

#### Create a new site for installation of other apps
bench new-site site1.local

### INSTALLING APPS (Execute 1 by 1)
$bench get-app payments<br>
$bench get-app --branch version-14 erpnext<br>
$bench get-app hrms<br>
$bench get-app ecommerce_integrations --branch main<br>
$bench --site site1.local install-app erpnext<br>
$bench --site site1.local install-app hrms

*If system is not able to install any of these apps then there might be a problem in installation
of python/mysql.*

## INITIALISING FRAPPE BENCH AND STARTING IT

#### Change directory to frappe bench:
$cd frappe-bench

*If permission is denied then:*
Chances are that you have switched to a new terminal and are not using sudo user that we have
created and given access to , so switch to the sudo user and then
give "cd .." command twice so that terminal appears like 
[sudouser]@ubuntu:/$ <br>
Now change directory to frappe bench


#### Start Bench Server
$bench start

*AND NOW YOU ARE ALL SET TO CREATE AN APP*


