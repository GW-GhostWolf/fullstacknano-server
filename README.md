# fullstacknano-server
Udacity Full Stack Nanodegree - Linux Server Configuration project

## Scenario
Take a Linux server from base installation to fully configured and secured web server. Take a baseline installation of a Linux distribution on a virtual machine and prepare it to host your web applications, to include installing updates, securing it from a number of attack vectors and installing/configuring web and database servers.

### Necessary Actions
I completed the following actions to configure my Linux server. You could use a Vagrant VM to do the same. I used Amazon Lightsail so that my server would be available on the internet.
* Update package list
* Upgrade all installed packages. 
* Change the default SSH port
* Configure key based authentication
* Install Apache web server, PostgreSQL, and python3
* Configure ports and enable firewall
* Configure PostgreSQL user and create database
* Add web files to the file system
* Configure Apache WSGI with python3
* Update Google OAuth to accept request and redirects from new server
* Run database initialization python script

### To the Grader
Server SSH: IP:2200\
Login: Grader\
Authorization: Key based sent separately\
Web Page: [http://IP/](http://google.com/)

#### Non Udacity Resources that Helped
* Page for configuring Apache with Flask
* PostreSQL documentation
