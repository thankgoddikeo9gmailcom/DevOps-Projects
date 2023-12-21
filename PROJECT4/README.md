# WEB STACK IMPLIMENTATION (LEMP STACK)

### sudo apt install nginx -y

[Title](README.md) ![Alt text](<Images/Screenshot 2023-12-07 042159.png>) ![Alt text](<Images/Screenshot 2023-12-07 042213.png>)

### Spin up an instance in AWS to run Nginx server, go to the security, then to the inbound rule configure http port 80 to enable the web page for the Nginx server to run on any browser.

[Title](README.md) ![Alt text](<Images/Screenshot 2023-12-07 042433.png>) ![Alt text](<Images/Screenshot 2023-12-07 042451.png>)

$ curl http://localhost:80
 or
$ curl http://127.0.0.1:80

[Title](README.md) ![Alt text](<Images/Screenshot 2023-12-07 042605.png>) ![Alt text](<Images/Screenshot 2023-12-07 042624.png>)

### $ ip address

![Alt text](<Images/Screenshot 2023-12-07 042752.png>)

### Go back to the AWS instance and copy the IP address (54.180.120.801.) and past it on a browser.

![Alt text](<Images/Screenshot 2023-12-07 051524.png>)

### To confirm that Nginx is working okay, I run command $ sudo systemctl status nginx

![Alt text](<Images/Screenshot 2023-12-07 073921.png>)

# STEP - 2 INSTALLING MYSQL SERVER

### run sudo apt install mysql-server -y

[Title](README.md) ![Alt text](<Images/Screenshot 2023-12-07 080540.png>) ![Alt text](<Images/Screenshot 2023-12-07 080551.png>)

### Loging into mysql by runing sudo mysql

### This will connect to MYSQL  as the admistative database user root  

![Alt text](<Images/Screenshot 2023-12-07 081055.png>)
![Alt text](<Images/Screenshot 2023-12-07 081701.png>)

# INSTALLING PHP

# $ sudo apt install php-fpm php-mysql

![Alt text](<Images/Screenshot 2023-12-07 082457.png>) ![Alt text](<Images/Screenshot 2023-12-07 082504.png>) 

# Configuring Nginx to use PHP processor

# $ sudo mkdir /var/www/projectLEMP

![Alt text](<Images/Screenshot 2023-12-07 084642.png>)

![Alt text](<Images/Screenshot 2023-12-15 035930.png>)

### Go back to the AWS instance and copy the Public IP and past it on the a browser.

![Alt text](<Images/Screenshot 2023-12-15 040735.png>)

# Testing PHP with Nginx

### Go back to the AWS instance and copy the Public IP/info.php and past it on the a browser.


![Alt text](<Images/Screenshot 2023-12-15 035954.png>)
![Alt text](<Images/Screenshot 2023-12-15 040004.png>)

# Retriving data from MYSQL database with PHP

# $ sudo mysql

# mysql> CREATE DATABASE `example_database`;

# mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';

![Alt text](<Images/Screenshot 2023-12-15 044500.png>)

### mysql> SHOW DATABASES;

![Alt text](<Images/Screenshot 2023-12-15 044720.png>)

### CREATE TABLE example_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));

### mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");

### mysql>  SELECT * FROM example_database.todo_list;

![Alt text](<Images/Screenshot 2023-12-15 045307.png>)

### mysql> exit

### $ nano /var/www/projectLEMP/todo_list.php

### http://<Public_domain_or_IP>/todo_list.php


![Alt text](<Images/Screenshot 2023-12-15 050201.png>)
![Alt text](<Images/Screenshot 2023-12-15 050828.png>)
![Alt text](<Images/Screenshot 2023-12-15 050843.png>)