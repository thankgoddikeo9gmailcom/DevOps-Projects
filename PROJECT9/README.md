# PROJECT 6

# TASK

### Prepare storage infrastructure on two Linux servers and implement a basic web solution using WordPress. WordPress is a free and open-source content management system written in PHP and paired with MySQL or MariaDB as its backend Relational Database Management System (RDBMS).

# Project 6 consists of two parts:

### Configure storage subsystem for Web and Database servers based on Linux OS. The focus of this part is to give you practical experience of working with disks, partitions and volumes in Linux.

### Install WordPress and connect it to a remote MySQL database server. This part of the project will solidify your skills of deploying Web and DB tiers of Web solution.

# Three-tier Architecture

### Generally, web, or mobile solutions are implemented based on what is called the Three-tier Architecture.

### Three-tier Architecture is a client-server software architecture pattern that comprise of 3 separate layers.
### Presentation Layer (PL): This is the user interface such as the client server or browser on your laptop.

### Business Layer (BL): This is the backend program that implements business logic. Application or Webserver

### Data Access or Management Layer (DAL): This is the layer for computer data storage and data access. Database Server or File System Server such as FTP server, or NFS Server

### Your 3-Tier Setup
### 1. A Laptop or PC to serve as a client

### 2. An EC2 Linux Server as a web server (This is where you will install WordPress)

### 3. An EC2 Linux server as a database (DB) server (This is where you will install myqsl-server)

# Step 1 — Prepare a Web Server

### 1. Launch an EC2 instance that will serve as "Web Server". Create 3 volumes in the same AZ as your Web Server EC2, each of 10 GiB. (RHEL-8.6.0_HVM-20220503-x86_64-2-Hourly2-GP2)

### 2. Attach all three volumes one by one to your Web Server EC2 instance

### 3. Open up the Linux terminal to begin configuration

[text](README.md) ![text](<Images/Screenshot 2024-04-26 065401.png>) ![text](<Images/Screenshot 2024-04-26 070422.png>) ![text](<Images/Screenshot 2024-04-26 070525.png>) ![text](<Images/Screenshot 2024-04-26 070824.png>)     

### 4. Run sudo yum update -y, to enable the configurations on the server to go well.

![text](<Images/Screenshot 2024-04-26 071624.png>)
![alt text](<Images/Screenshot 2024-04-26 071638.png>)

### 5. Use lsblk command to inspect what block devices are attached to the server. Notice names of your newly created devices. All devices in Linux reside in /dev/ directory. Inspect it with ls /dev/ and make sure you see all 3 newly created block devices there – their names will likely be xvdb, xvdc, and xvdd
## Run sudo ls /dev to see the directorieis is this location.

![alt text](<Images/Screenshot 2024-04-26 072731.png>)

### 6. Use df -h command to see all mounts and free space on your server

![alt text](<Images/Screenshot 2024-04-26 072903.png>)


### 7. Use gdisk utility to create a single partition on each of the 3 disks
### Run p,n,p and w to partion the three disk properly.

![alt text](<Images/Screenshot 2024-04-26 073052.png>)

### 8. Use lsblk utility to view the newly configured partition on each of the 3 disks

![alt text](<Images/Screenshot 2024-04-26 073628.png>)

### 9. Install lvm2 package using sudo yum install lvm2.

 ![text](<Images/Screenshot 2024-04-26 074703.png>) ![alt text](<Images/Screenshot 2024-04-26 074715.png>)

### Run sudo lvmdiskscan command to check for available partitions.

[text](README.md) ![text](<Images/Screenshot 2024-04-26 074911.png>) 

### Run sudo lvmdiskscan

### 10. Use pvcreate utility to mark each of 3 disks as physical volumes (PVs) to be used by LVM
### sudo pvcreate /dev/xvdb1
###	sudo pvcreate /dev/xvdc1
###	sudo pvcreate /dev/xvdd1

![text](<Images/Screenshot 2024-04-26 075050.png>) 

### 11. Run sudo pvs

![text](<Images/Screenshot 2024-04-26 075208.png>) 

### 12. Use vgcreate utility to add all 3 PVs to a volume group (VG). Name the VG webdata-vg

### sudo vgcreate webdata-vg /dev/xvdb1 /dev/xvdc1 /dev/xvdd1

### sudo vgs

![text](<Images/Screenshot 2024-04-26 075658.png>) 

### 13. Use lvcreate utility to create 2 logical volumes. apps-lv (Use half of the PV size), and logs-lv Use the remaining space of the PV size. NOTE: apps-lv will be used to store data for the Website while, logs-lv will be used to store data for logs.

### sudo lvcreate -n apps-lv -L 14G webdata-vg

###	sudo lvcreate -n logs-lv -L 14G webdata-vg

![text](<Images/Screenshot 2024-04-26 080003.png>)

### 14. Verify that your Logical Volume has been created successfully by running sudo lvs

[text](README.md) ![text](<Images/Screenshot 2024-04-26 080103.png>)

### 15. Verify the entire setup
###	sudo vgdisplay -v #view complete setup - VG, PV, and LV

 ![text](<Images/Screenshot 2024-04-26 080659.png>)
  ![text](<Images/Screenshot 2024-04-26 080714.png>) 
  
  ### sudo lsblk

  ![text](<Images/Screenshot 2024-04-26 080822.png>) 

  ### 16.Use mkfs.ext4 to format the logical volumes with ext4 filesystem

###	sudo mkfs -t ext4 /dev/webdata-vg/apps-lv

###	sudo mkfs -t ext4 /dev/webdata-vg/logs-lv 
  
  ![text](<Images/Screenshot 2024-04-26 084301.png>) 

  ### 17. Create /var/www/html directory to store website files

 ### sudo mkdir -p /var/www/html

 ### 18. Create /home/recovery/logs to store backup of log data

 ### sudo mkdir -p /home/recovery/logs

 ### 19. Mount /var/www/html on apps-lv logical volume

 ### sudo mount /dev/webdata-vg/apps-lv /var/www/html/

 ### 20. Use rsync utility to backup all the files in the log directory /var/log into /home/recovery/logs (This is required before mounting the file system)

 ### sudo rsync -av /var/log/. /home/recovery/logs/

 ![text](<Images/Screenshot 2024-04-26 084820.png>)
  
### 21. Mount /var/log on logs-lv logical volume. (Note that all the existing data on /var/log will be deleted. That is why step 17 above is very important)

### sudo mount /dev/webdata-vg/logs-lv /var/log

### Restore log files back into /var/log directory

   ![text](<Images/Screenshot 2024-04-26 085702.png>)

###	sudo rsync -av /home/recovery/logs/. /var/log


   [text](README.md) ![text](<Images/Screenshot 2024-04-26 085728.png>)
   
### Run lsblk

![alt text](<Screenshot 2024-05-04 162401.png>)

### 22. Update /etc/fstab file so that the mount configuration will persist after restart of the server.
## The UUID of the device will be used to update the /etc/fstab file;
### sudo blkid


 ![text](<Images/Screenshot 2024-04-26 195741.png>) 
 
### sudo vi /etc/fstab

### Update /etc/fstab in this format using your own UUID

 ![text](<Images/Screenshot 2024-04-26 200510.png>) 
 
### 23. Test the configuration and reload the daemon
###	sudo mount -a

###	sudo systemctl daemon-reload

### Verify your setup by running df -h


 ![text](<Images/Screenshot 2024-04-26 201004.png>) 
 
 ### Step 2 — Prepare the Database Server
### Launch a second RedHat EC2 instance that will have a role – ‘DB Server’

### Repeat the same steps as for the Web Server, but instead of apps-lv create db-lv and mount it to /db directory instead of /var/www/html/.


 ![text](<Images/Screenshot 2024-04-26 203734.png>) 
 
## Step 3 — Install WordPress on your Web Server EC2

### 1. Update the repository

### sudo yum -y update

### 2. Install wget, Apache and it’s dependencies

###    sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json

### 3. Start Apache

 ![text](<Images/Screenshot 2024-04-27 045315.png>) 
 ![text](<Images/Screenshot 2024-04-27 045323.png>) 

### 3. Start Apache

 ###   sudo systemctl enable httpd

###    sudo systemctl start httpd

###    sudo systemctl httpd status

 ![text](<Images/Screenshot 2024-04-27 045529.png>)
 
### To install PHP and it'S dependencies

### sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm

### sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-9.rpm

### sudo yum module list php

### sudo yum module reset php

### sudo yum module enable php:remi-7.4

### sudo yum install php php-opcache php-gd php-curl php-mysqlnd
	
### sudo systemctl start php-fpm

### sudo systemctl enable php-fpm

### sudo setsebool -P httpd_execmem 1

### 5. Restart Apache

### sudo systemctl restart httpd

  ![text](<Images/Screenshot 2024-04-27 050114.png>) 
  
  ![text](<Images/Screenshot 2024-04-27 050126.png>) 
  
### 6. Download wordpress and copy wordpress to var/www/html

### mkdir wordpress

### cd   wordpress

### sudo wget http://wordpress.org/latest.tar.gz
 
### sudo tar -xzvf latest.tar.gz
 
### sudo rm -rf latest.tar.gz
 
### sudo cp -R wordpress /var/www/html/

### sudo systemctl restart httpd

## cd into /var/www/html directory

### cd wordpress

	
### sudo cp wp-config-sample.php wp-config.php

### sudo wget http://wordpress.org/latest.tar.gz` downloads the file

### sudo tar -xzvf latest.tar.gz` uncompresses the file

### sudo rm -rf latest.tar.gz` deletes the compressed file and its content

### sudo cp -R wordpress/ /var/www/html/` will copy the directory wordpress recursively to /var/www/html directory. 

### cp wp-config-sample.php wp-config.php` this is creating another file wp-config.php which 
### contains the scipt which wordpress uses for installation.This contains database setting where to put the values 
### of the database user name, password, host name so that the webserver can be able to connect to the database server. 

  ![text](<Images/Screenshot 2024-04-27 050354.png>)

  [text](README.md) ![text](<Images/Screenshot 2024-04-27 050126.png>)
  
   ![text](<Images/Screenshot 2024-04-27 050354.png>) 

   ![text](<Images/Screenshot 2024-04-27 050412.png>) 

### 7. Configure SElinux Policies   

### sudo chown -R apache:apache /var/www/html/wordpress
### sudo chcon -t httpd_sys_rw_content_t /var/www/html/wordpress -R
 ### sudo setsebool -P httpd_can_network_connect=1

 ### Run ls /var/www/html


 ![text](<Images/Screenshot 2024-04-27 050913.png>) 
   
## Step-4 Install MYSQL on your DBserver EC2

### sudo yum update
### sudo yum install mysql-server

### Verify that the sysytem is up and runing by runing sudo systemctl status mysql, if it is not up and runing you will have to restart the service and enable it so it will be runing even after reboot.

![text](<Images/Screenshot 2024-04-30 054653.png>) 
   
![text](<Images/Screenshot 2024-04-30 054707.png>) 
   
###  sudo systemctl restart mysqld
###  sudo systemctl enable mysqld

### sudo systemctl status mysql

![text](<Images/Screenshot 2024-04-30 054914.png>) 
   
### Step 5. Configure DB to work with Wordpress

### sudo mysql
### CREATE DATABASE wordpress;
### CREATE USER 'myuser'@'Web-server-Private-IP-Address' IDENTIFIED BY 'mypass';
### GRANT ALL ON wordpress.* TO 'myuser'@'Web-server-Private-IP-Address';
### FLUSH PRIVILEGES;
### SHOW DATABASES;
### exit


![text](<Images/Screenshot 2024-04-30 064710.png>)
   
![text](<Images/Screenshot 2024-04-30 070224.png>) 
    
### Step 6. Configure  Wordpress to connect to remote DBserver

### Hint: Do not forget to open MYSQL port 3306. For extra security, you shall allow access to DBserver only from your webserver IP address, so in the inbound rule configuration specify sourec as /32

### 1. Install MYSQL-CLIENT and test that you can connect from your Webserver to your DB server by using mysql-client.

### sudo yum install mysql

### 2. Verify if you have successfully excute SHOW DATABSES; command and see a list of exiting data baseses;

### 3. Change permission and configuration so Apache could use Wordpress

### 4. Enable TPC port 80 in the inbound rule configuration for your Web server EC2 ( enable from everywhere 0.0.0.0/0 or from your work statio IP )

![text](<Images/Screenshot 2024-04-30 072101.png>) 
    
### sudo mysql -u admin -p -h DB-Server-Private-IP-address>

![text](<Images/Screenshot 2024-04-30 075604.png>) 
### Run ls /var/www/html

### Run cd /var/www/html

### Run ls -al

![text](<Images/Screenshot 2024-04-30 085017.png>) 
### cd ~

### cd /var/www/html

### ls wordpress/

![text](<Images/Screenshot 2024-04-30 092133.png>)
   
### Configure file wp-config.php to enable you gain access to wordprsess

### sudo vi wp-config.php


[text](README.md) ![text](<Images/Screenshot 2024-04-30 095220.png>) 

![text](<Images/Screenshot 2024-04-30 095233.png>) 

### Run sudo systemctl restart httpd

![text](<Images/Screenshot 2024-04-30 095905.png>)

### 2. Verify if you have successfully excute SHOW DATABSES; command and see a list of exiting data baseses;

### 3. Change permission and configuration so Apache could use Wordpress

### 4. Enable TPC port 80 in the inbound rule configuration for your Web server EC2 ( enable from everywhere 0.0.0.0/0 or from your work statio IP )

### Try to access your browser the link to your Wordpress http://web-server-public-IP-Address>/wordpress/

![text](<Images/Screenshot 2024-04-30 100436.png>)
 
![text](<Images/Screenshot 2024-04-30 100449.png>)
  
![text](<Images/Screenshot 2024-04-30 100552.png>)
   
![text](<Images/Screenshot 2024-04-30 100707.png>) 
    
![text](<Images/Screenshot 2024-04-30 100943.png>)

   ![text](<Images/Screenshot 2024-04-30 100957.png>)
