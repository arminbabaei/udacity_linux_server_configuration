# udacity_linux_server_configuration

1. The IP address and SSH port so your server can be accessed by the reviewer.
 
    35.183.32.239 -p 22
 
2. The complete URL to your hosted web application.
 
    35.183.32.239

3. A summary of software you installed and configuration changes made.

    List of sofwares installed 
    
    $ sudo apt-get update
    $ sudo apt-get upgrade
    $ sudo apt-get install apache2
    $ sudo apt-get install postgresql
    $ sudo apt-get install python-psycopg2
    $ sudo apt-get install libpq-dev python-dev
    $ sudo apt-get install libapache2-mod-wsgi-py3
    $ sudo apt-get install python3.6

    Create grader user 
    
    $ cat /etc/passwd
    $ sudo adduser grader
    $ sudo ls /etc/sudoers.d
    $ sudo vi /etc/sudoers.d/grader
    $ sudo passwd -e grader 
    
    Generating Key pairs				$ ssh-keygen 
    Installing Public Key
    (server side)
	   $ mkdir .ssh
	   $ touch .ssh/authorized_keys
    (client side)
   	$ cat ~/.ssh/id_rsa.pub
    (server side)
	   $ vi .ssh/authorized_keys
	   $ chmod 700 .ssh
	   $ chmod 644 .ssh/authorized_keys
    (client side)
	   $ ssh ubuntu@35.183.32.239
 
    Forcing Key Based Authentication		
    $ sudo vi /etc/ssh/sshd_config
				  PasswordAuthentication no
				$ sudo service ssh restart
        
    How to create the database 
    
    $ psql postgres
    postgres=# create database catalog;
    postgres=# create user catalog with encrypted password 'catalog';
    postgres=# grant all privileges on database catalog to catalog;
    postgres=# \q
    
    $ python models.py
    $ python data.py
    
    WSGI setting
    
    Create catalog.conf on server
    $ sudo vi /etc/apache2/sites-enabled/catalog.conf
    
    <VirtualHost *:80>
     ServerAdmin armin.babaei@gmail.com
     WSGIDaemonProcess catalog user=catalog group=www-data threads=5
     WSGIProcessGroup catalog
     WSGIScriptAlias / /var/www/udacity_item_catalog/catalog.wsgi
      <Directory /var/www/udacity_item_catalog/>
        Require all granted
      </Directory>
    </VirtualHost>
    
4. A list of any third-party resources you made use of to complete this project.

    Stach Overflow

