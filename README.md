# Linux_Server_Configuration



### i. The IP address and SSH port so your server can be accessed by the reviewer.
* IP address : 54.167.253.0
* SSH port : 2200

### ii. The complete URL to your hosted web application.
   * http://54.167.253.0

### iii. Summary of software you installed and configuration changes made.
##### 1.Update all installed packages
##### 2.Configure the Uncomplicated Firewall (UFW)

* default deny incoming
* default allow outgoing
* allow port 80/HTTP
* allow port 2200/SSH
* allow pott 123/NTP
* Change the SSH port from 22 to 2200


##### 3.Configure the local timezone to UTC.
##### 4.Create and configure user grader 
* add user grader (password: grader)
* Give grader the permission to sudo
* Create an SSH key pair for grader using the ssh-keygen tool.
* login as grader

##### 5.Install and configure Apache to serve a Python mod_wsgi application
apache2
libapache2-mod-wsgi
postgresql
python-pip

##### 6.Configure sites-enabled file and enable a new virtual host
```sh
 /etc/apache2/sites-enabled$ sudo nano 000-default.conf 
 ```
 Add the following to the 000-default.conf file
 ```sh
 WSGIScriptAlias / /var/www/item_catalog_beta/catalog.wsgi

<Directory /var/www/item_catalog_beta>

        Order deny,allow
        Allow from all

</Directory>

<Directory /var/www/item_catalog_beta/static>
        Order deny,allow
        Allow from all
</Directory>

Alias /static /var/www/item_catalog_beta/static

</VirtualHost>

 ```
##### 7.under /var/wwww/ Clone item_catalog_beta from github 
##### 8.Create a catalog.wsgi file and add the following into the file
 ```sh
 import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0, '/var/www/item_catalog_beta/')

from project import app as application
application.secret_key='secret_key'
 ```
 
##### 9.Install and configure PostgreSQL
* create user catalog (password:catalog)
* Do not allow remote connections
* create database catalog
* Change the setup in each file come with the database connection to the following
 ```sh
 engine = create_engine('postgresql://catalog:catalog@localhost/catalog')
 ```


##### 10.Install python packages
flask
sqlalchemy
requests

##### Locate the SSH key you created for the grader user.
/.ssh$ nano authorized_keys


### Resources:
1.Udacity discussion form
2.Digital Ocean
3.http://flask.pocoo.org/docs/0.10/deploying/mod_wsgi/
4.http://docs.sqlalchemy.org/en/latest/core/engines.html#postgresql
