# BASIC LINUX COMMANDS IMPLIMENTED ON GIT BASH TERMINAL #

### Command cd ~ is used to change directory on linux terminal while command ls is use to check on list of items such as directories/repository/folder, and files. ###

![Alt text](<Images/Screenshot 2023-10-23 113252.png>)

#### Change directory into downloads, cd downloads/ ####

![Alt text](<Images/Screenshot 2023-10-23 113325.png>)

Command chmod 400 otd-KEY.pem run to ensure the our key remains private only accessable to whoso ever we make available to.
In this project I connect to instance using its Public DNS: ssh -i "otd-KEY.pem" ubuntu@ec2-54-180-24-47.ap-northeast-2.compute.amazonaws.com.

![Alt text](<Images/Screenshot 2023-10-23 113418.png>)

As recommended by the system, I ran apt list --upgradable to upgrade the application software.

![Alt text](<Images/Screenshot 2023-10-23 113938.png>)

I ran command sudo apt-get install ubuntu-advantage-tools, as recommended by the system for flexibility in operating the th ubuntu.

![Alt text](<Images/Screenshot 2023-10-23 114225.png>)

I ran command Sudo pro status, to get the current status of to some detailed information.

![Alt text](<Images/Screenshot 2023-10-23 114443.png>)

I ran command cat "otd-KEY.pem" to view some hiden imformation/codes in the in the "otd-KEY.pem" file.

![Alt text](<Images/Screenshot 2023-10-23 114721.png>)

I ran command exit to logout from the present page into another page.

![Alt text](<Images/Screenshot 2023-10-23 171611.png>)

Command mkdir --help is to aid guid someone to carry out some operation and flag commands that may be required.

![Alt text](<Images/Screenshot 2023-10-23 172025.png>)

Command ping -c3 www.google.com is a head command to verify if a network is runing and command ping www.google.com which will run infinity unless terminated by ctrl C.

![Alt text](<Images/Screenshot 2023-10-23 172315.png>)

 sudo man ping command

 ![Alt text](<Images/Screenshot 2023-10-23 173137.png>)

 Command history will show all the commands one have used in a project or operation you are working on.

 ![Alt text](<Images/Screenshot 2023-10-23 173230.png>)

 pwd command meaning print working directory

 ![Alt text](<Images/Screenshot 2023-10-23 173559.png>)

 mkdir command is use to create a repository

 ![Alt text](<Images/Screenshot 2023-10-23 173818.png>)

 touch command is use to creat a file on terminal

 ![Alt text](<Images/Screenshot 2023-10-23 173845.png>)

 rm command is use to remove a file or files from terminal

 ![Alt text](<Images/Screenshot 2023-10-23 174007.png>)

 ll and ls -a command does almost the same thing, they show all hiden files and repositories wthin the working context.

 ![Alt text](<Images/Screenshot 2023-10-23 174034.png>)

![Alt text](<Images/Screenshot 2023-10-23 174611.png>)

cd . command means current directory

![Alt text](<Images/Screenshot 2023-10-23 174751.png>)

Command mkdir project1 project2, creates two repositories at the same time.

![Alt text](<Images/Screenshot 2023-10-24 041535.png>)

### The following Commands and proceedures discribed below are steps to create a folder inside another folder ###

mkdir linux-project then type command ls, cd into linux-project, and type ls, and then type mkdir git-project, type command pwd, then ls the git-project repository will pop up, cd into git-project, and type mkdir people, then type ls, the repository named people will pop up, making it sub folder inside a sub folder in folder called linux-project.

![Alt text](<Images/Screenshot 2023-10-24 042126.png>)

cd ../.. command is take you further backward into a page than the cd .

![Alt text](<Images/Screenshot 2023-10-24 042253.png>)

whoami command tells us the home host name that you are working on

users center command

![Alt text](<Images/Screenshot 2023-10-24 043042.png>)

sudo -i is a root command or a command to access into the root #

![Alt text](<Images/Screenshot 2023-10-24 043136.png>)
![Alt text](<Images/Screenshot 2023-10-24 043210.png>)

nano command is a command use to edit and write more file on terminal

![Alt text](<Images/Screenshot 2023-10-24 044127.png>)

sudo apt install cmatrix, is a command use installing cmatrix on a terminal

![Alt text](<Images/Screenshot 2023-10-24 044713.png>)

Suceesful installation of cmatrix

![Alt text](<Images/Screenshot 2023-10-24 044803.png>)

sudo apt install nginx -y command was use to install nginx on terminal

![Alt text](<Images/Screenshot 2023-10-24 045444.png>)

useradd is a command use to create a home account on the terminal, and you can name the account as you wish.

![Alt text](<Images/Screenshot 2023-10-24 045756.png>)

cat /etc/passwd command is use to access or read the informtion in a password file.

![Alt text](<Images/Screenshot 2023-10-24 051207.png>)

sudo useradd mary is a command use to create an acccount called mary.

- Note any normal user account you creat will always start from 1000

- Any application user account you create will will start from 1-999

- Admin user account will start from 0

- To switch into mary account run su - mary, and it will request for a password, then you will have to create one.
To put a pass word run sudo password mary

![Alt text](<Images/Screenshot 2023-10-24 052612.png>)
![Alt text](<Images/Screenshot 2023-10-24 052620.png>)
![Alt text](<Images/Screenshot 2023-10-24 055525.png>)

sudo adduser emma is the command I use to create a valid account for emma.

![Alt text](<Images/Screenshot 2023-10-24 061959.png>)
![Alt text](<Images/Screenshot 2023-10-24 062021.png>)