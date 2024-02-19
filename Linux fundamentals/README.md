# Linux Fundamentals

## System Information
- Find out the machine hardware name and submit it as the answer.
```sh
uname -i
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%201.JPG)

```sh
x86_64
```

- What is the path to htb-student's home directory?
```sh
pwd
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%202.JPG)

```sh
/home/htb-student
```

- What is the path to the htb-student's mail?
```sh
echo "$MAIL"
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%203.JPG)

```sh
/var/mail/htb-student
```

- Which shell is specified for the htb-student user?
```sh
echo "$SHELL"
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%204.JPG)

```sh
/bin/bash
```

- Which kernel version is installed on the system? (Format: 1.22.3)
```sh
uname -r
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%205.JPG)

```sh
4.15.0
```

- What is the name of the network interface that MTU is set to 1500?
```sh
ifconfig
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%206.JPG)

```sh
ens192
```

## Navigation
-  What is the name of the hidden "history" file in the htb-user's home directory?
```sh
ls -la
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%207.JPG)

```sh
.bash_history
```

- What is the index number of the "sudoers" file in the "/etc" directory?
```sh
ls -i /etc | grep sudoers
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%208.JPG)

```sh
147627
```

## Working with Files and Directories
- What is the name of the last modified file in the "/var/backups" directory?
```sh
ls -la -t /var/backups
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%209.JPG)

```sh
apt.extended_states.0
```

- What is the inode number of the "shadow.bak" file in the "/var/backups" directory?
```sh
ls -i /var/backups/shadow.bak
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2010.JPG)

```sh
265293
```

## Find Files and Directories
- What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?
```sh
find / -type f -name *.conf -newermt 2020-03-03 -size -28k -size +25k 2>/dev/null
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2011.JPG)

```sh
00-mesa-defaults.conf
```

- How many files exist on the system that have the ".bak" extension?
```sh
find / -type f -name *.bak 2>/dev/null | wc -l
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2012.JPG)

```sh
4
```

- Submit the full path of the "xxd" binary.
```sh
which xxd
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2013.JPG)

```sh
/usr/bin/xxd
```

## File Descriptors and Redirections
- How many files exist on the system that have the ".log" file extension? 
```sh
find / -type f -name *.log 2>/dev/null | wc -l
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2014.JPG)

```sh
32
```
- How many total packages are installed on the target system?
```sh
apt list --installed | grep -c "installed"
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2015.JPG)

```sh
737
```

## Filter Contents
- How many services are listening on the target system on all interfaces? (Not on localhost and IPv4 only)
```sh
netstat -tlpn | grep -v "127.0.0." | grep -v tcp6 | grep -c LISTEN
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2016.JPG)

```sh
737
```

- Determine what user the ProFTPd server is running under. Submit the username as the answer.
```sh
ps aux | grep proftpd
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2017.JPG)

```sh
proftpd
```