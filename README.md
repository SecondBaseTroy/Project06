# Project06
# for Full-Stack Web Developer
## by S.Hartmann 12/06/2018
## version 1.0

**Requirements**
- Webbrowser like Firefox or Chrome
- Developed and tested on Windows 10.x
- Used VM for Full-Stack Web Developer
- Flask
- sqlalchemy
- requests
- oauth2client for Google Login
- Project 04 - Item Catalog

**General Note**
Developed with MS VS Code
Referenced Stack Overflow, Python, SQLAlchemy, Bootstrap, w3resource, GitHub and other sites
- https://docs.sqlalchemy.org/en/latest/core/engines.html?highlight=create_engine#sqlalchemy.create_engine
- https://dba.stackexchange.com/questions/96368/creating-a-database-under-a-different-owner
- http://flask-sqlalchemy.pocoo.org/2.3/config/#connection-uri-format
- https://stackoverflow.com/questions/769683/show-tables-in-postgresql
- https://stackoverflow.com/questions/12720967/how-to-change-postgresql-user-password
- https://stackoverflow.com/questions/4313323/how-to-change-owner-of-postgresql-database
- https://stackoverflow.com/questions/44742566/wsgi-cant-find-file-in-same-directory-in-app
- https://docs.sqlalchemy.org/en/latest/core/engines.html?highlight=create_engine#sqlalchemy.create_engine
- https://docs.djangoproject.com/en/2.1/howto/deployment/wsgi/modwsgi/#using-mod-wsgi-daemon-mode
- https://modwsgi.readthedocs.io/en/develop/user-guides/quick-configuration-guide.html


Server Info
Server: 34.237.172.141
Access to VM via port 2200

Catalog Project
http://34.237.172.141.xip.io/catalog

This project uses Amazon Lightsail to create a Linux server instance.
Will need an account in Amazon Lightsail.

Log into Amazon Lightsail
- Create an OS instance
- Choose an OS instance: Ubuntu (OS only)
- Choose your lan (lowest tier is fine)
- Assign your OS instance a hostname
- Wait for creation of OS instance
-- Once the instance has started up, follow the instructions provided to SSH into your server.

Secure your server with by updating all currently installed packages.
- sudo apt-get update
- sudo apt-get upgrade

Change the SSH port from 22 to 2200. Make sure to configure the Lightsail firewall to allow it.
- sudo nano /etc/ssh/sshd_config
-- change port form 22 to 2200

 Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).
-  sudo ufw allow 2200/tcp
-  sudo ufw allow 80/tcp
-  sudo ufw allow 123/tcp
-  sudo ufw enable

Create an account 'grader' and grant access.
- sudo adduser grader

Give grader the permission to sudo.
- sudo nano /etc/sudoers.d/grader
- add text grader ALL=(ALL) NOPASSWD:ALL

Create an SSH key pair for grader using the ssh-keygen tool on local workstation.
- ssh-keygen -t rsa

To login
- ssh -i .ssh/grader_udacity grader@34.237.172.141 -p 2200

Configure the local timezone to UTC.
- sudo dpkg-reconfigure tzdata
-- select none of the above, then UTC

Install packages needed project
- sudo apt-get -qqy install postgresql python-psycopg2
- sudo apt-get install python-pip
- sudo pip install requests
- sudo pip install oauth2client
- sudo pip install htpplib2
- sudo apt-get -qqy install python-sqlalchemy
- pip install werkzeug
- pip install flask
- pip install Flask-Login
    
Install and configure Apache to serve a Python mod_wsgi application
- create catalog.wsgi file in /var/www/catalog and configure
- start up apache via command
- sudo a2ensite catalog

Install and config postgresql
- sudo apt-get install postgresql

Install Git
- sudo apt-get install git
- clone copy of project from Git and install it in /var/www/catalog

Create a new database named catalogshoe in Postgres
- see reference for details at https://www.postgresql.org/docs/9.1/manage-ag-createdb.html

Update database_load.py, database_config.py and project.py with Postgres engine vs SQLite
- engine = create_engine('postgresql://catalogow:stevepw@localhost/catalogshoe')

Configure Apache
- sudo nano/var/www/catalog/catalog.wsgi
- sudo apache2ctl restart

- sudo nano/etc/apache2/sites-available/catalog.conf
- sudo a2ensite catalog
- sudo service apache2 restart
