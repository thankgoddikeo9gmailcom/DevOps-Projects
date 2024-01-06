# Introduction To Shell Scripting And User Input. #

## Shell Scripting Syntax Elements.

### Assigning value to variable

name="John"

### Retriving value from variable

echo $name

![Alt text](<Images/Screenshot 2024-01-06 130504.png>)

### Example: Using if-else to execute script based on a condition.

![Alt text](<Images/Screenshot 2024-01-06 081915.png>)

### Example: Iterating through a list using a for loop.

![Alt text](<Images/Screenshot 2024-01-06 083756.png>)

## 3. Command subtitution

### Example: Using kickback for command subtitution

![Alt text](<Images/Screenshot 2024-01-06 085745.png>)

## 4. Input and Output:

### Accepting user input

echo "enter your name:"

read name

![Alt text](<Images/Screenshot 2024-01-06 090247.png>)

### Example: Output text to terminal

echo "Hello World"

![Alt text](<Images/Screenshot 2024-01-06 093344.png>)

### Example: Out the result of a file into a command.

echo "hello world" > index.txt


![Alt text](<Images/Screenshot 2024-01-06 094110.png>)

### Example: Pass the content of a file as input to a command.

grep "pattern" < input.txt

![Alt text](<Images/Screenshot 2024-01-06 094519.png>)

## 5. FUNCTION: Allow bash to to combine or group related commands together to easily run and automate scripting on bashshell.

![Alt text](<Images/Screenshot 2024-01-06 101238.png>)

# Let Write Our First Shell Script.

### 1. On the shell open a folder called shell-scriptiing, run mkdir shell-scriptiing this will hold all the script we will write.

### 2. Create a file called user-input.sh using command touch user-input.sh.

### 3. Copy and past the codes inside the file you created called user-input.sh.

### 4. Save your file.

### 5. Run the command sudo chmod +x user-input.sh this makes it executable.

### 6. Run the script using the command ./user-input.sh

![Alt text](<Images/Screenshot 2024-01-06 102240.png>)

# Directory Manipulation and Navigation.

## Directory Manipulation and Navigation.

### This script will display the current directory, creat a new directory called "My_directory," change to that directory, creat two files insde it, list the files, move back one level up, remove the "My_directory" and its contents, and finally list the files in the mew or current directory again.

### Following the steps below:

### 1. Create a file called navigating-linux-filesystem.sh

### 2. Past the copied code.

### 3. Run the command sudo chmod +x navigating-linux-filesystem.sh to set execution permission on the file.

### 4. Run your script using his command ./navigating-linux-filesystem.sh

![Alt text](<Images/Screenshot 2024-01-06 103648.png>)
![Alt text](<Images/Screenshot 2024-01-06 104012.png>)

## File Operating And Sortiing.

### File Operating And Sortiing.

### This script creates three files (file1.txt, file2.txt, file3.txt), displays the files in there current order, sorts them alphabetically, saves the sorted files in the sorted_files.txt, displays the contents of the final sorted file.

### Step 1. Open your terminal and create a file called sorting.sh, using a command touch sorting.sh.

### Step 2. Copy and past the code block below.

### Step 3. Run the command sudo chmod +x sorting.sh

### Step 4. Run the script, using the command ./sorting.sh

![Alt text](<Images/Screenshot 2024-01-06 110838.png>)
![Alt text](<Images/Screenshot 2024-01-06 110919.png>)

# Working With Numbers And Calculations.

## Working With Numbers And Calculations.

### This script defines two variables num1 and num2, with numeric values, performs basice arithmetic oerations (addition, subtraction, multiple, dvision, and modules), and displays the results, it also performs more complex calculations such as raising num1 to the powe of 2, and calculate the square root ot num2, and displays those results as well.

### Following the below steps:

### Step 1. On your terminal creat a file called calculation.sh, using the command touch calculation.sh.

### Step 2. Copy and past the code block below.

### Step 3. Set execution permission on calculation.sh, usint the command sudo chmod +x calculation.sh.

### Step 4. Run your script using the command ./calculation.sh

![Alt text](<Images/Screenshot 2024-01-06 112133.png>)
![Alt text](<Images/Screenshot 2024-01-06 112302.png>)
![Alt text](<Images/Screenshot 2024-01-06 112510.png>)

# File Backup And Timestamping.

## File Backup And Timestamping.

### This scripting focused on file backupand timestamp. As a DevOps Engineer, backing up database and other storage devices is one of the most common task you get to carryout. 

### This scripting defines the source of directory paths, it then create a timestamp using the current date and time, and create a backup directory with the timestamp apendined to its name, the script then copies all files from the source direcrory to the backup directory using the cp command with the -r option for recursive copying. Finally it displays the message indicating the completion of the backup process and shows the path of the backup directory with the timestamp.

### Following the steps below:

### Step 1. On your terminal create a file called backup.sh, using the command touch backup.sh.

### Step 2. Copy and past the code block below into the file you created using any of the file editor, nano or vim.

### Step 3. Set executution permission on backup.sh, using the command sudo chmod +x backup.sh

### Step 4. Run the script using the command ./backup.sh

![Alt text](<Images/Screenshot 2024-01-06 115029.png>)
![Alt text](<Images/Screenshot 2024-01-06 115115.png>)
![Alt text](<Images/Screenshot 2024-01-06 115159.png>)
![Alt text](<Images/Screenshot 2024-01-06 121250.png>)