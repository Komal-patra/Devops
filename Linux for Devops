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
