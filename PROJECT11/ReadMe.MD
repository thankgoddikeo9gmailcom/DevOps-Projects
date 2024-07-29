# Ansible Automatiomation project
### sible and why use IT?
### Ansible is an open source, command-line IT automation software application written in Python.

### It can configure systems, deploy software, and orchestrate advanced workflows to support application deployment, system updates, and more.

### Ansible's main strengths are simplicity and ease of use.

### - Ansible is an automation engine that helps us to automate tasks that are cumbersome, repititive and complex. It makes work easier for the DevOps department.

### - Ansible Client as a Jump Server (Bastion Host)
### A Jump Server (sometimes also referred as Bastion Host) is an intermediary server through which access to internal network can be provided.

### With the current architecture I will be working on, ideally, the webservers would be inside a secured network which cannot be reached directly from the Internet.

### That means, even DevOps engineers cannot SSH into the Web servers directly and can only access it through a Jump Server - it provides better security and reduces attack surface.

### On the diagram below the Virtual Private Network (VPC) is divided into two subnets - Public subnet has public IP addresses and Private subnet is only reachable by private IP addresses.

### ![alt text](image.png)



# What is configuration management?
### Configuration management is a process for maintaining computer systems, servers, applications, network devices, and other IT components in a desired state. It’s a way to help ensure that a system performs as expected, even after many changes are made over time.

### Using configuration management tools, administrators can set up an IT system, such as a server or workstation, then build and maintain other servers and workstations with the same settings. IT teams use configuration assessments and drift analyses to continuously identify systems that have strayed from the desired system state and need to be updated, reconfigured, or patched.

### https://www.redhat.com/en/topics/automation/what-is-configuration-management#:~:text=Configuration%20management%20is%20a%20process,in%20a%20desired%2C%20consistent%20state.&text=Managing%20IT%20system%20configurations%20involves,building%20and%20maintaining%20those%20systems

### How to Install and Configure Ansible Client to act as a Jump Server/Bastion Host and Create a simple Ansible Playbook to automate server configuration

## Prerequistes:

### 1. NFS Server
### 2.Web Server 1
### 3. Web Server 2
### 4. Load Balancer
### 5. Database Server
### 6. Jenkins Server
### The following steps are taken to install and configure Ansible Client as a Jump Server/Bastion Host and create a simple Ansible Playbook to automate server configuration:

### Install and configure ansible on ec2 instance.

### 1. Update the Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. We will use this server to run playbooks.

![text](<Images/Screenshot 2024-07-03 154656 - Copy - Copy.png>) 
![text](<Images/Screenshot 2024-07-03 154656 - Copy.png>)
![text](<Images/Screenshot 2024-07-03 154656.png>) 
![text](<Images/Screenshot 2024-07-03 155341.png>) 
![text](<Images/Screenshot 2024-07-03 160155.png>)

## Create a new repository called ansible-config-mgt in your GitHub account.

### https://github.com/thankgoddikeo9gmailcom/Ansible-config-mgt.git

![text](<Images/Screenshot 2024-07-03 160806.png>)
![text](<Images/Screenshot 2024-07-03 160953.png>) 
![text](<Images/Screenshot 2024-07-03 161346.png>)

### sudo apt update -y

### sudo apt install ansible -y

![text](<Images/Screenshot 2024-07-03 161614.png>) 
![text](<Images/Screenshot 2024-07-03 161926.png>)

### Ansible --version

![text](<Images/Screenshot 2024-07-03 162131.png>) 
 
### It is important to note that Jenkins wont work until Java is installed, hence, we need to install Java language before you can use Jenkins

### sudo apt install openjdk-17-jre-headless

![text](<Images/Screenshot 2024-07-03 162722.png>) 

### To check whether Java is installed, run the below command;

### java

![text](<Images/Screenshot 2024-07-03 162848.png>) 
![text](<Images/Screenshot 2024-07-03 162901.png>)

 To install Jenkins, run the below commands; REF: https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

 ###### sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
##### https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

##### echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
##### https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
##### /etc/apt/sources.list.d/jenkins.list > /dev/null

### sudo apt-get update

### sudo apt-get install jenkins

! [text](<Images/Screenshot 2024-07-03 163603 copy.png>)
![text](<Images/Screenshot 2024-07-03 163603.png>) 
![text](<Images/Screenshot 2024-07-03 163608.png>) 

### sudo systemctl status jenkins

![text](<Images/Screenshot 2024-07-03 163649 copy.png>) 

### sudo cat /var/lib/jenkins/secrets/initialAdminPassword
 
### To get the password to setup jenkins-server

![text](<Images/Screenshot 2024-07-03 163914.png>)
![text](<Images/Screenshot 2024-07-03 164608.png>) 
![text](<Images/Screenshot 2024-07-03 164902.png>) 
![text](<Images/Screenshot 2024-07-03 165156.png>)
![text](<Images/Screenshot 2024-07-03 165615.png>) 
![text](<Images/Screenshot 2024-07-03 165647.png>)
![text](<Images/Screenshot 2024-07-03 165659.png>)

## Configure Jenkins build job to archive your repository content every time you change it.

### Create a new Freestyle project ansible in Jenkins and point it to your 'ansible-config-mgt' repository.
Click on the caption "New Item" as shown in the below screenshot

![text](<Images/Screenshot 2024-07-04 235143.png>) 
![text](<Images/Screenshot 2024-07-04 235330.png>) 
![text](<Images/Screenshot 2024-07-05 000325.png>)
![text](<Images/Screenshot 2024-07-05 000559.png>)
![text](<Images/Screenshot 2024-07-05 001009.png>) 
![text](<Images/Screenshot 2024-07-05 001133.png>)
![text](<Images/Screenshot 2024-07-05 002054.png>)

## Clone your repository down to your VSC CLI terminal

### Configure a Post-build job to save all (**) files.

### Configure a webhook in GitHub and set the webhook to trigger ansible build.

![text](<Images/Screenshot 2024-07-05 013950.png>)
![text](<Images/Screenshot 2024-07-05 014032.png>)
![text](<Images/Screenshot 2024-07-05 014534.png>)
![text](<Images/Screenshot 2024-07-05 014605.png>) 
![text](<Images/Screenshot 2024-07-05 014620.png>)
![text](<Images/Screenshot 2024-07-05 014805.png>) 
![text](<Images/Screenshot 2024-07-05 015532.png>)
![text](<Images/Screenshot 2024-07-05 015542.png>)
![text](<Images/Screenshot 2024-07-05 015605.png>) 

## Built success on Jenkins

![text](<Images/Screenshot 2024-07-05 022751.png>) 
![text](<Images/Screenshot 2024-07-05 022804.png>) 
![text](<Images/Screenshot 2024-07-05 023534.png>)
![text](<Images/Screenshot 2024-07-05 131750.png>)
![text](<Images/Screenshot 2024-07-05 132436 copy.png>) 

## Begin Ansible Developent

### sudo mkdir inventory playbooks

### cd playbooks, and creat file with command touch common.yml

### cd inventory, 

### cd inventory, and create files, with command touch dev.yml staging.yml uat.yml prod.yml

![text](<Images/Screenshot 2024-07-05 145618.png>) 

## Create a mommon playbooks.
### Time to start giving the instruction you want it to perform the servers listed in inventory/dev.yml.

### In common.yml, playbooks will write configuration for repeatable, re-usable multi-machine task that is common to the system within the infrastructure.

### Update inventory/dev.yml with the following codes:

#### [nfs]
<NFS-Server-Private-IP-Address> ansible_ssh_user=ec2-user

[webservers]
<Web-Server1-Private-IP-Address> ansible_ssh_user=ec2-user
<Web-Server2-Private-IP-Address> ansible_ssh_user=ec2-user

[db]
<Database-Private-IP-Address> ansible_ssh_user=ec2-user 

[lb]
<Load-Balancer-Private-IP-Address> ansible_ssh_user=ubuntu


![text](<Images/Screenshot 2024-07-10 032257.png>) 


### update the playbooks/common.yml

##### ---
##### - name: update web, nfs and db servers
  ##### hosts: webservers, nfs, db
  ##### become: yes
  ##### tasks:
##### - name: ensure wireshark is at the latest version
   #####  yum:
   ##### name: wireshark
 ##### state: latest
   

##### - name: update LB server
 #####  hosts: lb
  ##### nbecome: yes
  ##### tasks:
   ##### - name: Update apt repo
   ##### apt: 
   ##### update_cache: yes 
   ##### - name: ensure wireshark is at the latest version
   ##### apt:
   #####  name: wireshark
   ##### state: latest

![alt text](<Screenshot 2024-07-28 201939-1.png>)

### eval `ssh-agent -s`

### ssh-add Jenkins-Ansible.pem

### using ssh agentwe now connect to our Jenkins-Ansible server with the below command.

### ssh -A <ubuntu@public ip address> the Jenkins-Ansible server

![text](<Images/Screenshot 2024-07-16 153153.png>) 
![text](<Images/Screenshot 2024-07-16 153915.png>) 

### ssh-add -l

![text](<Images/Screenshot 2024-07-16 154046.png>) 

### ssh into the LB server with the below command.

### ssh ubuntu@LB ip address

![text](<Images/Screenshot 2024-07-16 155249.png>) 

### ls /var/lib/jenkins/jobs/ansible/builds/5/archive/

![text](<Images/Screenshot 2024-07-17 064700.png>) 
![text](<Images/Screenshot 2024-07-17 064725.png>) 

### git status

### git add .

### git commit -m "made some changes"

### git push origin prj-11

![text](<Images/Screenshot 2024-07-18 055205.png>)
![text](<Images/Screenshot 2024-07-18 060710.png>) 
![text](<Images/Screenshot 2024-07-18 060747.png>)

## Github account below;

### compare & pull request, and merge it.

![text](<Images/Screenshot 2024-07-18 061323.png>) 
![text](<Images/Screenshot 2024-07-18 061654.png>)
![text](<Images/Screenshot 2024-07-18 061711.png>) 
![text](<Images/Screenshot 2024-07-18 061720.png>) 

### Edit and configure the security, section in the AWS 

![text](<Images/Screenshot 2024-07-22 020532.png>) 

### sudo apt install wirehark -y

![text](<Images/Screenshot 2024-07-24 101515.png>) 

### wireharkt --version

![text](<Images/Screenshot 2024-07-24 101630.png>) 

### git pull origin prg-11

![text](<Images/Screenshot 2024-07-24 110309.png>) 
![text](<Images/Screenshot 2024-07-24 155052.png>) 

### ls /var/lib/jenkins/jobs/ansible/build/5/archive

### cd  /var/lib/jenkins/jobs/ansible/build/5/archiv

### ls

### cd into inventory

### cat inventory

### cd into playbooks

### cat playbooks

![text](<Images/Screenshot 2024-07-24 164753.png>) 
![text](<Images/Screenshot 2024-07-24 164802.png>) 

# Run first ansible test

### cd ansible-config-mgt

###  /var/lib/jenkins/jobs/ansible/build/5/archiv~$ ansible-playbook -i inventory/dev.yml playbooks/common.yml

### assible automation run successfully


![text](<Images/Screenshot 2024-07-25 194938.png>) 
![text](<Images/Screenshot 2024-07-25 194953.png>) 
![text](<Images/Screenshot 2024-07-25 195952.png>) 
![text](<Images/Screenshot 2024-07-25 201434.png>)