# WEB STACK IMPLIMENTATION (LAMP STACK) IN AWS ###

### Connet to the instance by runing, ssh -i "SERVERKEY.pem" ubuntu@ec2-51-20-140-74.eu-north-1.compute.amazonaws.com

![Alt text](<Images/Screenshot 2023-12-04 115753.png>)33

### Run sudo apt update, to update the server to enable install technological tools that will be used in the CLI or teminal.

sudo apt install apache2, to install a web page or web server

![Alt text](<Images/Screenshot 2023-12-04 145842.png>)
![Alt text](<Images/Screenshot 2023-12-04 145857.png>)
### spin up an instance in AWS

![Alt text](<Images/Screenshot 2023-12-04 125526.png>)

### Go to security to inbound rule to enable pot 80 in other for Apache2 web page to be configured correctly. copy the public IP and past it in any web server and Apache2 web page pops up.

![Alt text](<Images/Screenshot 2023-12-04 150039.png>)

### run a command, pin localhost to confirm if the Apache2 server is working efficiently.

![Alt text](<Images/Screenshot 2023-12-04 150322.png>)

### curl localhost command is run to further confirm that the Apache2 server is runing 

![Alt text](<Images/Screenshot 2023-12-04 150413.png>)![Alt text](<Images/Screenshot 2023-12-04 150423.png>)

### IP address was run to confirm the computer IP address

![Alt text](<Images/Screenshot 2023-12-04 151923.png>)

# INSTALLING MYSQL

### sudo apt install mysql-server -y, command is applied on the teminal to achieve the installation of Mysql. It an application that help to store and manage database in web server.

![Alt text](<Images/Screenshot 2023-12-06 063607.png>)![Alt text](<Images/Screenshot 2023-12-06 063618.png>)

### sudo mysql command will connect the mysql server as the addmistrative database user root

![Alt text](<Images/Screenshot 2023-12-06 090611.png>)

### To remove insecur default setting this security script is run, ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';

### Then exit msql

### sudo mysql_secure_installtion, command is run, then you will be asked to insert your own chioce of pass word.

![Alt text](<Images/Screenshot 2023-12-06 131240.png>)![Alt text](<Images/Screenshot 2023-12-06 133110.png>)

# INSTALLING PHP

### apache2 is been installed to serve content, mysql is also been installed to store and and manage data. PHP is the set up conponent that wll process code to display dynamic of the content to the end user (customer). In addition to php other modules like (php-mysql) is needed to be installed that will allow php to communicate with mysql effectively and (libapache2-mod-php) to handle apache2 files. The following commands are run.

#### Installing a three in one package I run ( $ sudo apt install php libapache2-mod-php php-mysql
)
![Alt text](<Images/Screenshot 2023-12-06 134017.png>)![Alt text](<Images/Screenshot 2023-12-06 134051.png>)

### To confirm the version of php install I run php -v

![Alt text](<Images/Screenshot 2023-12-06 134133.png>)

# At this stage LAMP STACK is completely installed and fully operational.

# ENABLE PHP ON THE WEBSITE.

## With the default directory of apache2 file named index.html that has precedence of index.php, will have to be reconfigured allow the enabling of the php set up code content by the command below.

### sudo vim /etc/apache2/mods-enabled/dir.conf

#### <IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>

### Save the file and reload apache2

![Alt text](<Images/Screenshot 2023-12-06 140555.png>)

#### Now that we have a location to host our website files and folders we will creat a php test scrip to confirm that apache2 is able to handl and process request for php files.

### mkdir index.html is applied to Creat a file named index.html.

### $ vim /var/www/projectlamp/index.php

### <?php
phpinfo();
 is applied. Save and close the file editor, and check your web browser.

 ![Alt text](<Images/Screenshot 2023-12-06 140735.png>)
 ![Alt text](<Images/Screenshot 2023-12-07 032712.png>)

 

 # Creating a Vitual Host For Your Website Using Apache2

 ### Create a directory mkdir projectlamp

 ### $ sudo mkdir /var/www/projectlamp
### assign ownership of the directory $ USER environment variable which will reference your current system user.

### $ sudo chown -R $USER:$USER /var/www/projectlamp

### Create a new configuration file apache's available site.

### $ sudo vi /etc/apache2/sites-available/projectlamp.conf

### A blank file is created, the past the copied script commands.

### <VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

### Save and close the file using the following steps, esc, :,wq w for write, q for quit, then enter.

### $ sudo ls /etc/apache2/sites-available
You will see something like this
000-default.conf  default-ssl.conf  projectlamp.conf

### $ sudo a2ensite projectlamp
, is used to enable the virtual website

### $ sudo a2dissite 000-default
Is used to disable the site.

### To ensure no configuration error is incured I run 

### $ sudo apache2ctl configtest

### The new websit is now active but the virtual root /var/www/projectlamp/ is still empty. Create an index.html in that location to test that theh site is working as expected by runing the command.

### sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html


