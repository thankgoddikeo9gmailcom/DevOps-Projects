# Automating Load balancer with shell scripting.

## Streamline your load balancer configuration with eas by using shell scripting and simple CI/CD jenkins. This project illustrate how to set-up and maintain your load balancer using a freestyle jobs, enhancing efficiency and reducing manual efforts.

# Automate the deployment of web servers.

### In the implementing load balancer with nginx in this course, I us two backend webservers with a load balancer distributing loads across the webservers. I achieved that by typing commands on my terminal environment.

### In this course I will be automating ther entire process. I will do that by writing a shell script, and then ran, all that I did in the prceeding project manually will be done automatically. As a DevOps engineer automation is at the heart of what we practice.

### Automation help us speed up service delivery and reduce mistakes and errors in our day to day activities.

# Deploying and configuring the webservers.

### Below are the steps followed:

### Step 1: Launch an instance runing on ubuntu 20.04.

 ![text](<Images/Screenshot 2024-02-17 090813.png>) ![text](<Images/Screenshot 2024-02-17 090840.png>)

### Step 2: Open a security group on port 8000, to allow trafics from anywhere.

 ![text](<Images/Screenshot 2024-02-17 090930.png>) ![text](<Images/Screenshot 2024-02-17 091032.png>)

 ### Step 3: Connect to the two webservers, Web 1 and Web2 using SSH Client on your terminal.

 ![alt text](<Images/Screenshot 2024-02-17 091444.png>)

 ### I Changed the host name to Web1 and Web2 respectively in order to suit this project by runing the command below;

 ### Sudo vi /etc/hostname

### The command, Sudo reboot now; ensure that the changes made takes effect. 

 ![text](<Images/Screenshot 2024-02-17 091655.png>) ![text](<Images/Screenshot 2024-02-17 091901.png>)

### Step 4: Create a file named install.sh, by runing the below command and past the script.

### Sudo vi /install.sh

![alt text](<Images/Screenshot 2024-02-17 092138.png>)

### Next I run the command to confirm that a file is been created.

### cat install.sh


![alt text](<Images/Screenshot 2024-02-17 093055.png>)


### Step 5: Change the permmission on the file to make an executabel using the command below:

### sudo chmod +x install.sh

![alt text](<Images/Screenshot 2024-02-17 093544.png>)

### Step 6: Run the shell script using the below command. 

###  ./install.sh 51.20.1.85:8000,     ./install.sh 16.171.154.86:8000


 ![text](<Images/Screenshot 2024-02-17 093544.png>) ![text](<Images/Screenshot 2024-02-17 093603.png>)

### Next I run the command below to comfirm locally that the webservers are working okay.

### curl localhost:8000

 ![alt text](<Images/Screenshot 2024-02-17 093752.png>)

 ### Next I run the following command to further confirm that the web1 and web2 are working okay.

 ### ping localhost.

 ![alt text](<Images/Screenshot 2024-02-17 093941.png>)

### Next I copy and past the pulic_IP:8000 run on my webrowser, below is the out put/results for both webservers, web1 and web2 respectively.

 ![text](<Images/Screenshot 2024-02-17 094200.png>) ![text](<Images/Screenshot 2024-02-17 094215.png>)

# Deployment of Nginx as a load balancer using shell script.

## Automate the deployment of Nginx as a load balancer using shell script.

### Having successfully deployed and configured two webservers, I moved on to the load balancer. As a prerequisite, we need to provision and EC2 instance runing on Ubuntu 22.04, open on port 80 to anywhere using the security group and connect to the load balancer via my terminal.

# Deploying and configuring Nginx as a load balancer.

## Steps to run the scripts:

### Step 1: Connect to my instance with the below command.

### $ ssh -i "load.pem" ubuntu@ec2-16-171-182-133.eu-north-1.compute.amazonaws.com

![alt text](<Images/Screenshot 2024-02-17 094502.png>)

### I changed the host name by runing the below commands:

### sudo vi /etc/hostname

### tO ensure that the made takes effect, i  run the below command.

### sudo reboot now 

![alt text](<Images/Screenshot 2024-02-17 094759.png>)

### Runing the script.

### Step 1: Open a file named; nginx.sh on my terminal with the command, then copy, past the script and run the script.

### sudo vi /nginx.sh

![alt text](<Images/Screenshot 2024-02-17 131726.png>)

### cat the file.

### cat nginx.sh

 ![text](<Images/Screenshot 2024-02-17 095004.png>) ![text](<Images/Screenshot 2024-02-17 095012.png>)

### Next I run the command

### sudo chmod +x nginx.sh

### ./nginx.sh PUBLIC_IP WEB1 PUBLIC_IP:8000 WEB2 PUBLIC_IP:8000

### ./nginx.sh 16.171.182.133 51.20.1.85:8000 16.171.154.86:8000

 [text](README.md) ![text](<Images/Screenshot 2024-02-17 095728.png>) ![text](<Images/Screenshot 2024-02-17 095741.png>)

### Next copy and past the public_IP for the load balancer, web1 and web2 on your OS webrowser I have the following results.

![text](<Images/Screenshot 2024-02-17 095924.png>) ![text](<Images/Screenshot 2024-02-17 095936.png>) ![text](<Images/Screenshot 2024-02-17 095950.png>)