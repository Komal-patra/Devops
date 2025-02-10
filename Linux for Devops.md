## DevOps

---

# Linux Commands

## Switching Users

### Changing from EC2 to Root User:
```sh
sudo -i
# OR
sudo su -
```

### Changing from Root to EC2 User:
```sh
logout
# OR
ctrl + d
```

---

## System Information

### Check CPU Information:
```sh
cat /proc/cpuinfo
# OR
lscpu
```

### Check Memory (RAM) Information:
```sh
cat /proc/meminfo
# OR
lsmem
```

### Check ROM (Volume) Information:
```sh
fdisk -l
# OR
lsblk
# OR
df -m
```

### Find IP Address of the Server:
```sh
ifconfig
# OR
hostname -I
# OR
ip addr show
```

---

## File Commands

### Create a File:
```sh
touch filename
```

### Show List of Files:
```sh
ls
# OR
ll
# OR
ls -ltr
```

### Show Content of a File:
```sh
cat filename
```

### Insert Content into a File:
```sh
cat >> filename  # Press 'ctrl + d' to exit
```

### Copy Content from One File to Another:
```sh
cp file1 file2
# 'cp' automatically creates file2 if it does not exist
```

### Rename a File:
```sh
mv file1 file2
```

### Remove a File:
```sh
rm filename
```

### Remove All Files in a Directory:
```sh
rm * -f
```

### Create Multiple Files:
```sh
touch file{1..100}
```

### Append Content of file1 to file2 (without overwriting file2):
```sh
cat file1 >> file2
```

---

## System Performance

### Check Server Performance:
```sh
top  # Press 'q' to exit
# OR
htop  # Requires installation: yum install htop -y
```

---

## File Viewing

### View First Few Lines of a File:
```sh
head filename  # Default 10 lines
head -n 20 filename  # View first 20 lines
```

### View Last Few Lines of a File:
```sh
tail filename  # Default 10 lines
tail -n 20 filename  # View last 20 lines
```

### Read a Large File Page-by-Page:
```sh
less filename
# OR
more filename
```

---

## Directory Management

### Show Current Directory:
```sh
pwd
```

### Create a Directory:
```sh
mkdir directory_name
```

### Remove a Directory:
```sh
rmdir directory_name
# OR
rm -r directory_name/
```

### Change Directory:
```sh
cd directory_name
```

### Move to Previous Directory:
```sh
cd -
```

---

## Other Commands

### Count Words in a File:
```sh
wc filename
```

### Create a Soft Link (Symbolic Link):
```sh
ln -s filepath newfilename
# Example:
ln -s /home/ec2-user/cloud/softandhardlink softlinkfile
```

### Create a Hard Link:
```sh
ln filepath newfilename
# Example:
ln /home/ec2-user/cloud/softandhardlink hardlinkfile
```

### Compare Differences Between Two Files:
```sh
diff file1 file2
```

---

# Editor Commands

## Open a File in Editor:
```sh
vi filename
# OR
vim filename
```

## Insert Mode:
```sh
i  # Enter insert mode
```

## Exit Insert Mode and Save:
```sh
Press ESC, then type :wq
```

## Major Modes in Vi/Vim:

### 1. Command Mode:
```sh
Shift + G  # Go to last line
:set number  # Show line numbers
:n  # Go to line number n
```

### 2. Insert Mode:
```sh
i  # Insert mode
A  # Go to end of line
o  # New line below
O  # New line above
```

### 3. Save Mode:
```sh
:w  # Save
:q  # Quit
:wq  # Save and quit
:wq!  # Force save and quit
```

---

# Permissions

## File Permission Format:
```sh
-rw-r--r--
```

## File Types:
```sh
-  # Regular file
b  # Blocked file
c  # Character file
d  # Directory
l  # Link file
```

## Permission Values:
```sh
r (read)  = 4
w (write) = 2
x (execute) = 1
```

## Changing File Permissions:
```sh
chmod 7 filename  # Full permissions
chmod 6 filename  # Read & write
chmod 4 filename  # Read-only
chmod u=rw,g=rx,o=rwx filename  # Alphabetical format
```

## Ownership:
```sh
sudo chown username filename
sudo chgrp groupname filename
```

---

# System Level Commands
```sh
uname  # Platform name
uptime  # System uptime
whoami  # Active user
who  # User login history
which python  # Get installation path
id  # User ID
```

## User Management:
```sh
sudo useradd -m username  # Add user
sudo passwd username  # Change password
su username  # Switch user
sudo userdel username  # Delete user
```

---

# File Compression
```sh
sudo yum install zip  # Install zip
zip -r newfile.zip folder/  # Zip file/folder
unzip foldername  # Unzip file
```

## TAR Commands:
```sh
tar -cvzf file.tar.gz folder/  # Compress

tar -xvzf file.tar.gz  # Extract
```

---

## File Transfer

### Transfer File from Local to Remote:
```sh
scp -i "devops_komi_key.pem" localfilepath ec2-user@ec2-54-216-160-7.eu-west-1.compute.amazonaws.com:remotefile_path
```

---

## Networking Commands

### Check if Application is Responding:
```sh
ping urlname
```

### Show All Active Internet Connections:
```sh
netstat
# OR
ss
```

### Check Network Interface Card (NIC) Details:
```sh
ifconfig
```

### Trace Route to an Application:
```sh
traceroute application_name
# Example:
traceroute youtube.com
```

### Alternative Tracepath Command:
```sh
tracepath youtube.com
```

### Use MTR for Network Path Analysis:
```sh
mtr application_name
# Example:
mtr youtube.com   # Press 'q' to exit
```

### Show Active IP Address for an Application:
```sh
nslookup application_name
# Example:
nslookup google.com
```

### Show Hostname of Current System:
```sh
hostname
```

### Show IP Address of Laptop:
```sh
ip address show
```

### Get Detailed Information about an Application:
```sh
dig application_name
```

---

## AWK (Data Extraction for Formatted Files)

### Extract Specific Columns:
```sh
awk '{print $1}' app.log
awk '{print $1, $2, $3}' app.log
```

### Filter Logs by Keyword:
```sh
awk '/INFO/ {print $1, $2, $3, $5}' app.log
```

### Count Occurrences of INFO:
```sh
awk '/INFO/ {count++} END {print count}' app.log
```

### Extract Logs Between Time Range:
```sh
awk '$2 >= "08:52:00" && $2<= "08:53:00" {print $2, $3, $4, $5}' app.log
```

---

## SED (Stream Editor for Unformatted Data)

### Extract Lines Containing INFO:
```sh
sed -n '/INFO/p' app.log
```

---

## GREP (Global Regular Expression Print)

### Search for a Word in a File:
```sh
grep INFO filename.log
```

### Find Count of Occurrences:
```sh
grep INFO -i -c filename.log
```
