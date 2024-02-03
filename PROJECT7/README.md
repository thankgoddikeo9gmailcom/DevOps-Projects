# Implementing Loadbalancer With Nginx

### Discover the act of load balancing with Nginx, I learn how to distribute trafic across multiple servers, optimize performance and ensures high availabilities for your web applications.

### Step 1 & 2: Provisioning instances, and opened port 8000 for for the two web servers to listen from anywhere while the load balancer is opened with port 80

 ![Alt text](<Image/Screenshot 2024-02-02 084647.png>) ![Alt text](<Image/Screenshot 2024-02-02 084704.png>)

 ### Step 3:  

 ### I ssh  into my the aws instance on my terminal using the command, 

### ssh -i "WEB.pem" ubuntu@ec2-13-51-86-74.eu-north-1.compute.amazonaws.

 ![Alt text](<Image/Screenshot 2024-02-02 084716.png>)
 
 ### Next I run the command;

 ### sudo apt update -y &&  sudo apt install apache2 -y, to install apache2  on the to on both servers.
 
  ![Alt text](<Image/Screenshot 2024-02-02 084943.png>)
  ![Alt text](<Image/Screenshot 2024-02-02 084959.png>)

  ### To verify that apache2 is successfly installed and active, I run the below command.

  ### $ sudo systemctl status apache2, look at what I had.

![Alt text](<Image/Screenshot 2024-02-02 195946.png>)

### Step 4: Configure apache to serve a page showing it's publis IP address.

### I configured apache2 to serve content on port 8000, instead of the default port 80. Then I created a index.html file. The file will contain code to display the public IP of the EC2 instance, then I override the apache2 webserver default html file with my new file.

### Configure apache2 to serve content on port 8000.

### Step 1: run the below command.

### $ sudo vi /etc/apache2/ports.conf 

[Title](README.md) ![Alt text](<Image/Screenshot 2024-02-02 200437.png>) ![Alt text](<Image/Screenshot 2024-02-02 200457.png>)

### Next I open the file /etc/apache2/sites-available/000-default.conf, and port 80 virtual host to 8000, and run the below command.

### $ sudo vi /etc/apache2/sites-available/000-default.conf



[Title](README.md) ![Alt text](<Image/Screenshot 2024-02-02 201116.png>) ![Alt text](<Image/Screenshot 2024-02-02 201131.png>)

### I restart the apache2 to enable the any changes made to become effective, I run the command below;

### $ sudo systemctl restart apache2

![Alt text](<Image/Screenshot 2024-02-02 201357.png>)

## Creating a html file, I run the command

### $ sudo vi index.html

### Next step: switch the vi editor to insert mode and past the html file, get the public IP of the AWS EC2 instances and replace the placeholder text for IP address in the html file.

![Alt text](<Image/Screenshot 2024-02-02 201526.png>)
![Alt text](<Image/Screenshot 2024-02-02 201846.png>)

### I Changed the ownership of the html file with the command below:

### $ sudo chown www-data:www-data ./index.html

### To override the default html file of apache2, I run the command.

### $ sudo cp -f ./index.html /var/www/html/index.html

### Restart the apache2 to enable any change made to take effect, I run the command below;

### $ sudo systemctl restart apache2

![Alt text](<Image/Screenshot 2024-02-02 204659.png>)

### A page of this kind poped up so:

[Title](README.md) ![Alt text](<Image/Screenshot 2024-02-02 231221.png>) ![Alt text](<Image/Screenshot 2024-02-02 231230.png>)

### Next step: Configuring Nginx as a load balancer

### Launch another instance on AWD management console, ensure that it is configure for port 80, ssh into the instance to connect to the server, with the hostname load balancer with the aid of,

### $ sudo vi /etc/hostname/loadbalancer

### I run the below command to install Nginx.

### $ sudo apt update -y && sudo apt install nginx -y

![Alt text](<Image/Screenshot 2024-02-02 231559.png>) ![Alt text](<Image/Screenshot 2024-02-02 231612.png>)

### I run the below command to comfir that Nginx is up, active and runing.

### $ sudo systemctl status nginx

![Alt text](<Image/Screenshot 2024-02-02 231654.png>)

### Open Nginx configuration file with the command below.

### $ sudo vi /etc/nginx/conf.d/loadbalancer.conf

### Past the configurationfile to make Nginx to act as a load balancer. Ensure to edit and make all the neccary changes required, like your public IP address. 

![Alt text](<Image/Screenshot 2024-02-02 232022.png>)
![Alt text](<Image/Screenshot 2024-02-02 232040.png>) [Title](README.md) 

Upstream backend servers define a group of backend server.The server lines inside the upstream block list the address and port of your backend servers. The proy_set_header lines passes necesary header to the backend servers to correctly handle the request.

### Test the configuration with the command below:

### $ sudo nginx -t

### $ Restart the Nginx with the command below:

### $ sudo systemctl restart nginx

![Alt text](<Image/Screenshot 2024-02-02 232412.png>)

### Next, past the public IP address of the load balancer, the same webpages servered by the load balancer webserver poped up.

 ![Alt text](<Image/Screenshot 2024-02-03 003346.png>) ![Alt text](<Image/Screenshot 2024-02-03 003356.png>)



