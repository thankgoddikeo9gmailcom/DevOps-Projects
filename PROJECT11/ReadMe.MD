# Ansible Automatiomation project

## - What is Ansible and why use IT?

#### Ansible is an open source, command-line IT automation software application written in Python.

#### It can configure systems, deploy software, and orchestrate advanced workflows to support application deployment, system updates, and more.

#### Ansible's main strengths are simplicity and ease of use.

#### - Ansible is an automation engine that helps us to automate tasks that are cumbersome, repititive and complex. It makes work easier for the DevOps department.

#### - Ansible Client as a Jump Server (Bastion Host)
#### A Jump Server (sometimes also referred as Bastion Host) is an intermediary server through which access to internal network can be provided.

#### With the current architecture I will be working on, ideally, the webservers would be inside a secured network which cannot be reached directly from the Internet.

#### That means, even DevOps engineers cannot SSH into the Web servers directly and can only access it through a Jump Server - it provides better security and reduces attack surface.

#### On the diagram below the Virtual Private Network (VPC) is divided into two subnets - Public subnet has public IP addresses and Private subnet is only reachable by private IP addresses.

![alt text](<ansible setup (1).jpg>)

# What is configuration management?
#### Configuration management is a process for maintaining computer systems, servers, applications, network devices, and other IT components in a desired state. It’s a way to help ensure that a system performs as expected, even after many changes are made over time.

#### Using configuration management tools, administrators can set up an IT system, such as a server or workstation, then build and maintain other servers and workstations with the same settings. IT teams use configuration assessments and drift analyses to continuously identify systems that have strayed from the desired system state and need to be updated, reconfigured, or patched.

#### https://www.redhat.com/en/topics/automation/what-is-configuration-management#:~:text=Configuration%20management%20is%20a%20process,in%20a%20desired%2C%20consistent%20state.&text=Managing%20IT%20system%20configurations%20involves,building%20and%20maintaining%20those%20systems

#### How to Install and Configure Ansible Client to act as a Jump Server/Bastion Host and Create a simple Ansible Playbook to automate server configuration

## Install and configure ansible on ec2 instance.

## Step 1. Install and configure ansible on ec2 instance.
#### 1. update the name tag on your Jenkins ec2 instance to Jenkins-Ansible. We will use this server to run our playbooks.

#### 2.In your github account create a new repository and and name it ansible-config-mgt.

#### 3. Install ansible


#### Prerequistes:

#### 1. NFS Server
#### 2.Web Server 1
#### 3. Web Server 2
#### 4. Load Balancer
#### 5. Database Server
#### 6. Jenkins Server
#### The following steps are taken to install and configure Ansible Client as a Jump Server/Bastion Host and create a simple Ansible Playbook to automate server configuration:

# Step 1. Install and configure ansible on ec2 instance

## Install and Configure Ansible on EC2 Instance
#### 1. Update the Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. We will use this server to run playbooks.


![alt text](<Screenshot 2024-08-16 145949.png>)

## Update the Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. This server will be used to run playbooks.

### Install Ansible on the Jenkins-Ansible server.

#### https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

#### sudo apt update

#### sudo apt-get install ansible -y


![alt text](<Screenshot 2024-08-13 060206.png>)

![alt text](<Screenshot 2024-08-13 060328.png>) 
 
![alt text](<Screenshot 2024-08-13 060341.png>)

#### Confirm that Ansible is installed successfully

#### Check your Ansible Version by running the below command


#### ansible --version
 
![alt text](<Screenshot 2024-08-13 060419.png>) 
  
 #### 2. Create a new repository called ansible-config-mgt in your GitHub account.
#### https://github.com/thankgoddikeo9gmailcom/ansible-config-mgt.git

![alt text](<Screenshot 2024-08-13 060650.png>) 
  
![alt text](<Screenshot 2024-08-13 060709.png>)
  
#### It is important to note that Jenkins wont work until Java is installed, hence, we need to install Java language before you can use Jenkins

#### sudo apt install openjdk-17-jre-headless


![alt text](<Screenshot 2024-08-13 062735.png>) 
   
#### To check whether Java is installed, run the below command;

#### java

![alt text](<Screenshot 2024-08-13 062818.png>) 
   
#### To install Jenkins, run the below commands; REF: https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

 #### sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
   #### https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key


 #### echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  #### https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
   #### /etc/apt/sources.list.d/jenkins.list > /dev/null


   #### sudo apt-get install jenkins -y

![alt text](<Screenshot 2024-08-13 062946.png>) 
   
![alt text](<Screenshot 2024-08-13 063240.png>) 

 #### Run the below command to ensure that jenkins is up and runing.

#### sudo systemctl status jenkins

![alt text](<Screenshot 2024-08-13 063311.png>) 

#### In order to access ansible through the web browser, go to your EC2 instance inbound rule and open TCP port 8080, IPV4 anywhere
   
![alt text](<Screenshot 2024-08-13 063452.png>) 
   
![alt text](<Screenshot 2024-08-13 063605.png>) 
   
#### To setup an administrative password for my jenkins, run the below steps;

### sudo cat /var/lib/jenkins/secrets/initialAdminPassword

![alt text](<Screenshot 2024-08-13 063704.png>) 
   
![alt text](<Screenshot 2024-08-13 063756.png>) 
   
![alt text](<Screenshot 2024-08-13 064110.png>) 

![alt text](<Screenshot 2024-08-13 064226.png>) 

![alt text](<Screenshot 2024-08-13 064239.png>) 

![alt text](<Screenshot 2024-08-13 064315.png>) 

#### 4. Configure Jenkins build job to archive your repository content every time you change it.
### this will solidify your Jenkins configuration skills acquired in Project 9.
#### Log into Jenkins.

#### http://public_ip_jenkins_ansible_instance:8080
#### Create a new Freestyle project ansible in Jenkins and point it to your 'ansible-config-mgt' repository.
#### Click on the caption "New Item" as shown in the below screenshot

 ![alt text](<Screenshot 2024-08-13 071505.png>)
   
![alt text](<Screenshot 2024-08-13 071517.png>)
    
![alt text](<Screenshot 2024-08-13 071530.png>) 

![alt text](<Screenshot 2024-08-13 071543.png>) 

![alt text](<Screenshot 2024-08-13 071600.png>) 

# Configure a Post-build job to save all (**) files.
#### Configure a webhook in GitHub and set the webhook to trigger ansible build.

![alt text](<Screenshot 2024-08-15 075502.png>)

![alt text](<Screenshot 2024-08-15 082500.png>)
 
![alt text](<Screenshot 2024-08-15 083201.png>)
  
![alt text](<Screenshot 2024-08-15 092608.png>) 
   
![alt text](<Screenshot 2024-08-15 092851.png>)
   
![alt text](<Screenshot 2024-08-15 092858.png>)

#### 5. Test your setup by making  some changes in your README.md file in master branch and make sure that build starts automatically and Jenkins save the  file (build artifacts) in the following folder.

#### ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/
    
#### ls /var/lib/jenkins/jobs/ansible/builds/4/archive/

![alt text](<Screenshot 2024-08-15 093016.png>) 

![alt text](<Screenshot 2024-08-15 093343.png>) 

![alt text](<Screenshot 2024-08-15 093531.png>) 

## Step 2: Prepare your development environment using Visual Studio Code

#### - Download and install VS Code

#### - After successfully installing VS Code, configure it to connect to your newly created GitHub repository.

#### - Clone down the ansible-config-mgt repository to your local machine.

#### - git clone <ansible-config-mgt-repository-link>
#### Git Clone from Git Hub Repo

#### Step 5. Test your setup by making  some changes in your README.md file in master branch and make sure that build starts automatically and Jenkins save the  file (build artifacts) in the following folder.

#### ls /var/lib/jenkins/jobs/ansible/builds/<build_number>/archive/

## Begin Ansible Development.

### Step 3. Begin Ansible Development.
#### 1. In your ansible-config-mgt githup repositoyry, create a new branch that will be used for devolopment of a new feature

#### 2. Checkout the newly created feature branch to your local machine and start building your codes and directory structures.

#### 3. Create a directory call it playbooks, it will be used to store all your directory files.

#### 4. Create a directory call it inventory, it will be used to keep your organized.

#### 5. Within the playbooks folder, create your first playbooks files and name it common.yml

#### 6. Within the inventory folder, create an inventory file for each environment (Development, Staging, Testing and Prodouction) dev, staging, uat, and prod, respectively. 

![alt text](<Screenshot 2024-08-15 114026.png>) 

![alt text](<Screenshot 2024-08-15 114036.png>) 

![alt text](<Screenshot 2024-08-15 114219.png>) 

## Step 4. Setup an Ansible Inventory.

#### An inventory file define the host and group of hosts upon which commands, moudles, and task in a playbook operate. Hence the intension is to execute linux command in a remote host, and ensure it is the intended configuration on a particular server that occures. It is important to organize our host in such invetory.

#### Save the below inventory structure in inventory/dev file to start configuring your development servers. Ensure to replace the IP address according to your own set up.

## Note: That ansible uses port 22 by default, which means it has to ssh into a target server from Jenkins-Ansible host,  for this you can impliment the concept of ssh agent. Noe you need to import your key into ssh-agent.

#### eval `ssh-agent -s`

#### ssh-add <path-to-private-key>

#### ssh-add -l 

#### ssh -A ubuntu@public-ip

![alt text](<Screenshot 2024-08-15 122320.png>) 

![alt text](<Screenshot 2024-08-15 122652.png>) 

![alt text](<Screenshot 2024-08-15 122700.png>) 

![alt text](<Screenshot 2024-08-15 123230.png>) 
s
![alt text](<Screenshot 2024-08-15 123712.png>) 

![alt text](<Screenshot 2024-08-15 124033.png>) 

## Step 5. Create A Common Playbook

#### Create a common playbook

#### update yorur inventory/dev with the below codes.

---
- name: update web, nfs and db servers
  hosts: webservers, nfs, db
  become: yes
  tasks:
    - name: ensure wireshark is at the latest version
      yum:
        name: wireshark
        state: latest
   

 - name: update LB server
  hosts: lb
  become: yes
  tasks:
    - name: Update apt repo
      apt: 
        update_cache: yes

    - name: ensure wireshark is at the latest version
      apt:
        name: wireshark
        state: latest


![alt text](<Screenshot 2024-08-15 124252.png>) s

## Step 6. Update Git with the latest code.

#### Now all your directories and files lives in yoour local machine you need to push all the changes made to Github.

#### Now that you have a separate branch you will need to will need to know how to raise a pull request PR, get your branch peer reviewed and merge to the master branch.

#### Commit your code to Github.

#### 1. Use git command to add, commit and push your branch to Github.

#### git status

#### git add <selected files>

#### git commit -m "commit message"

#### git push origin prj-11

#### 2. Create a pull request, (PR)
#### 3. Wear the hat of another developer for a second and act as a reviewer

#### 4. If the reviewer is happy with your new feature deveopment, merge the code to the master branch.

#### 5. Head back to your terminal and checkout from the feature branch into the master and pull down the latest changes.

#### Once your code change appear in the master- Jenkins will do it's job and save all the file (build artifact) to /var/lib/jenkins/jobs/Ansible/builds/buil_number/archive directory on Jenkin-Ansible server.

![alt text](<Screenshot 2024-08-15 134743.png>) 

![alt text](<Screenshot 2024-08-15 134758.png>) 

![alt text](<Screenshot 2024-08-15 134820.png>) 

![alt text](<Screenshot 2024-08-15 135024.png>) 

![alt text](<Screenshot 2024-08-15 135138.png>) 

![alt text](<Screenshot 2024-08-15 135159.png>) 

![alt text](<Screenshot 2024-08-15 135222.png>) 

![alt text](<Screenshot 2024-08-15 135302.png>) 

![alt text](<Screenshot 2024-08-15 135332.png>) 

![alt text](<Screenshot 2024-08-15 135400.png>) 

### Build suceesful

![alt text](<Screenshot 2024-08-15 135707.png>) 

![alt text](<Screenshot 2024-08-15 135814.png>) 

#### To confirm that all the file where correctly created in the  /var/lib/jenkins/jobs/Ansible/builds/5/archive, I run the below commands:

#### cd  /var/lib/jenkins/jobs/Ansible/builds/buil_number/archive

#### ls

#### cd inventory

#### ls 

#### cat dev.yml

#### Repeat the same steps for playbooks folder.

![alt text](<Screenshot 2024-08-15 140938.png>) 

#### 5. Head back to your terminal and checkout from the feature branch into the master and pull down the latest changes.

![alt text](<Screenshot 2024-08-15 141815.png>) 

## Run First Ansible Test.

#### Step 7-Run First Ansible Test. 

#### Now it is time to execut ansible playbook command and verify if your playbooks actually works.

#### Set up yoru VSCODE to connect to your instance. Use the below commands

#### cd ansible-config-mgt

#### ansible-playbook -i inventory/dev.yml playbooks/common.yml


![alt text](<Screenshot 2024-08-15 150231.png>) 

![alt text](<Screenshot 2024-08-15 150322.png>) 

#### Verify that wirehark is install in each of the server with the below command.

#### wirehark --version

![alt text](<Screenshot 2024-08-15 154627.png>) 

#### ansible-playbook -i inventory/dev.yml playbooks/common.yml

![alt text](<Screenshot 2024-08-15 211442.png>) 

![alt text](<Screenshot 2024-08-15 211453.png>) 

#### Optional steps-repeat once again:

#### Update the ansible playbooks with some new ansible tasks and go through the full; checkout -->>>change codes --->>> commit --->>> PR --->>> merge --->>> build --->>> ansible playbook

![alt text](<Screenshot 2024-08-16 134525.png>) 

![alt text](<Screenshot 2024-08-16 134542.png>) 

![alt text](<Screenshot 2024-08-16 134604.png>) 

![alt text](<Screenshot 2024-08-16 134615.png>) 

![alt text](<Screenshot 2024-08-16 134628.png>) 

![alt text](<Screenshot 2024-08-16 134639.png>) 

![alt text](<Screenshot 2024-08-16 134648.png>) 

![alt text](<Screenshot 2024-08-16 134716.png>)

![alt text](<Screenshot 2024-08-16 134729.png>)
 
![alt text](<Screenshot 2024-08-16 134908.png>)
  
### Build sucessfully

![alt text](<Screenshot 2024-08-16 134923.png>)

# Sucessful

#### You have just automated to other servers by using ansible

#### Below is the artechture of the system.
![alt text](<Great Job.png>)