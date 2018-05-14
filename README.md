# fullstacknano-server
Udacity Full Stack Nanodegree - Linux Server Configuration project

## Scenario
Take a Linux server from base installation to fully configured and secured web server. Take a baseline installation of a Linux distribution on a virtual machine and prepare it to host your web applications, to include installing updates, securing it from a number of attack vectors and installing/configuring web and database servers.

### Necessary Actions
I completed the following actions to configure my Linux server. You could use a Vagrant VM to do the same. I used Amazon Lightsail so that my server would be available on the internet.
* Update package list and upgrade installed packages
```
sudo apt-get update
sudo apt-get upgrade
```
* Configure key based authentication
  * Create ~/.ssh/authorized_keys for each user
  ```
  mkdir -p ~/.ssh 
  touch ~/.ssh/authorized_keys
   ```
  * Add public keys to authorized_keys file (one key per line)
  * Set permissions on .ssh folder and authorized_keys file
  ```
  sudo chmod 700 ~/.ssh
  sudo chmod 644 ~/.ssh/authorized_keys
  ```
* Edit SSH configuration ```sudo nano /etc/ssh/sshd_config```
  * Disable password login ```PasswordAuthentication no```
  * Change ssh port ```Port 2200```
  * Restart ssh ```service sshd restart``` -- Note: verify key authentication and new ssh port before reseting or you will not be able to access the server
* Install Apache web server, PostgreSQL, and python3
```
sudo apt-get install apache2 postgresql python3 python3-pip libapache2-mod-wsgi-py3 git
sudo pip3 install --upgrade pip
sudo pip3 install --upgrade setuptools
sudo pip3 install flask sqlalchemy psycopg2 
```
* Configure ports and enable firewall
```
sudo ufw allow http
sudo ufw allow ntp
sudo ufw allow tcp/2200
sudo ufw enable
```
* Configure PostgreSQL user and create database
```
sudo passwd postgres
su postgres
psql
create role catalog with login password '******';
create database catalog with owner=catalog;
\q
exit
```
* Add web files to the file system
```git clone https://GW-GhostWolf@github.com/GW-GhostWolf/fullstacknano-catalog.git --branch CatalogWithPostgreSql```
* Configure Apache WSGI with python3 - see reference link in the Non Udacity Resources
  * View apache error logs ```sudo tail -f /var/log/apache2/error.log```
  * Restart apache server ```sudo /etc/init.d/apache2 restart```
* Update Google OAuth to accept request and redirects from new server
* Run database initialization python script
```python3 db_initialize.py```

### To the Grader
Server SSH: 18.221.22.163:2200\
Login: Grader\
Authorization: Key based sent separately\
Web Page: [http://18.221.22.163.xip.io/](http://18.221.22.163.xip.io/)

#### Non Udacity Resources that Helped
* [Configurat Key Based Authentication](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server#disabling-password-authentication-on-your-server)
* [Configuring Apache with Flask](https://jackhalpinblog.wordpress.com/2016/08/27/getting-your-python-3-flask-app-to-run-on-apache/)
* [PostreSQL documentation](https://www.postgresql.org/docs/10/static/index.html)
