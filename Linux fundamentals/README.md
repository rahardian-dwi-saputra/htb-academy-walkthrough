# Linux Fundamentals
- Link modul: https://academy.hackthebox.com/module/details/18
- Jalankan mesin target

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/setup%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/setup%202.JPG)

- Akses mesin dengan SSH
```sh
ssh htb-student@ip_mesin
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/setup%203.JPG)

## System Information
- **Question:** Find out the machine hardware name and submit it as the answer.
- Perintah `uname -a` digunakan untuk mencetak semua informasi tentang mesin yang digunakan dalam urutan nama kernel, nama host, rilis kernel, versi kernel, nama perangkat keras, dan sistem operasi. Untuk hasil spesifik bisa gunakan opsi `-i` untuk mencetak informasi hardware saja
```sh
uname -i
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%202.JPG)

- **Answer**
```sh
x86_64
```

- **Question:** What is the path to htb-student's home directory?
- Prompt bash terdiri dari rangkaian `<username>@<hostname><current working directory>$`. Home direktori pengguna dinotikasi dengan `~` yang merupakan folder default saat kita masuk melalui SSH. Untuk melihat path lengkap dimana posisi kita berada saat ini bisa gunakan perintah `pwd`
```sh
pwd
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%203.JPG)

- **Answer**
```sh
/home/htb-student
```

- **Question:** What is the path to the htb-student's mail?
- Perintah `env` dapat digunakan untuk mencetak seluruh informasi enviroment variable. Tapi jika kita ingin mencetak enviroment variable tertentu bisa gunakan perintah `echo "$nama_variabel"`
```sh
echo "$MAIL"
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%204.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%205.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%206.JPG)

- **Answer**
```sh
/var/mail/htb-student
```

- **Question:** Which shell is specified for the htb-student user?
```sh
echo "$SHELL"
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%207.JPG)

- **Answer**
```sh
/bin/bash
```

- **Question:** Which kernel version is installed on the system? (Format: 1.22.3)
- Gunakan opsi `-r` untuk mencetak versi kernel
```sh
uname -r
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%208.JPG)

- **Answer**
```sh
4.15.0
```

- **Question:** What is the name of the network interface that MTU is set to 1500?
- Ada beberapa variasi perintah untuk mencetak seluruh informasi network interface dengan format yang berbeda seperti `ip a` dan `ifconfig -a`
```sh
ifconfig -a
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%209.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2010.JPG)

- **Answer**
```sh
ens192
```

## Navigation
- **Question:** What is the name of the hidden "history" file in the htb-user's home directory?
- Untuk melihat daftar file dan direktori bisa menggunakan perintah `ls` kemudian tambahkan opsi `-a` untuk melihat daftar secara keseluruhan termasuk yang disembunyikan (hidden) dan opsi `-l` untuk mencetak daftar per baris secara lengkap 
```sh
ls -la
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2011.JPG)

- **Answer**
```sh
.bash_history
```

- **Question:** What is the index number of the "sudoers" file in the "/etc" directory?
- Gunakan opsi `-i` pada perintah `ls` untuk menampilkan index number tiap file dan direktori di direktori `/etc` lalu tambahkan filter pencarian dengan perintah `grep` untuk menampilkan nama file atau direktori yang mengandung kata `sudoers` 
```sh
ls -i /etc | grep sudoers
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2012.JPG)

- **Answer**
```sh
147627
```

## Working with Files and Directories
- **Question:** What is the name of the last modified file in the "/var/backups" directory?
- Gunakan opsi `-t` pada perintah `ls` untuk mengurutkan file dan direktori berdasarkan waktu modifikasinya. Yang terbaru akan tampil di bagian paling atas
```sh
ls -lat /var/backups
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2013.JPG)

- **Answer**
```sh
apt.extended_states.0
```

- **Question:** What is the inode number of the "shadow.bak" file in the "/var/backups" directory?
- Gunakan opsi `-i` pada perintah `ls` untuk menampilkan inode number atau index number
```sh
ls -i /var/backups/shadow.bak
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2014.JPG)

- **Answer**
```sh
265293
```

## Find Files and Directories
- **Question:** What is the name of the config file that has been created after 2020-03-03 and is smaller than 28k but larger than 25k?
- Gunakan perintah `find` untuk mencari sebuah file. Kita akan mencari melalui direktori root (/) agar bisa mencari secara keseluruhan. Tambahkan input `-type f` untuk tipe pencarian file. Lalu input `-name *.conf` karena file konfigurasi di linux pasti berekstensi `.conf`. Selanjutnya tambahan input `-newermt 2020-03-03` untuk menandakan bahwa file tersebut dibuat setelah tanggal 3-3-2020 dan tambahan input `-size -28k -size +25k` untuk menandakan file tersebut berukuran kurang dari 28k dan lebih dari 25k. Terakhir tambahan input `2>/dev/null` agar pesan error seperti `permission denied` tidak ditampilkan dihasil pencarian 
```sh
find / -type f -name *.conf -newermt 2020-03-03 -size -28k -size +25k 2>/dev/null
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2015.JPG)

- **Answer**
```sh
00-mesa-defaults.conf
```

- **Question:** How many files exist on the system that have the ".bak" extension?
- Tambahkan perintah `wc -l` untuk menghitung berapa baris file yang ditampilkan setelah hasil pencarian file menggunakan perintah `find`
```sh
find / -type f -name *.bak 2>/dev/null | wc -l
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2016.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2017.JPG)

- **Answer**
```sh
4
```

- **Question:** Submit the full path of the "xxd" binary.
- Perintah `which` akan menampilkan path program jika program tersebut tersedia. Namun jika tidak ditemukan maka perintah tersebut tidak akan menghasilkan output apapun
```sh
which xxd
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2018.JPG)

- **Answer**
```sh
/usr/bin/xxd
```

## File Descriptors and Redirections
- **Question:** How many files exist on the system that have the ".log" file extension? 
```sh
find / -type f -name *.log 2>/dev/null | wc -l
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2019.JPG)

- **Answer**
```sh
32
```
- **Question:** How many total packages are installed on the target system?
- Perintah `apt list --installed` akan menampilkan daftar package yang terinstall kemudian gunakan perintah `grep -c "installed"` untuk menghitung berapa banyak package yang yang terinstall
```sh
apt list --installed | grep -c "installed"
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2020.JPG)

- **Answer**
```sh
737
```

## Filter Contents
- **Question:** How many services are listening on the target system on all interfaces? (Not on localhost and IPv4 only)
- Untuk mencetak daftar service yang listening di jaringan bisa gunakan perintah `netstat -tlpn` dimana opsi `-t` berarti tcp, opsi `-l` berarti listening, opsi `-p` berarti program, dan opsi `-n` berarti numeric. Tambahan perintah `grep -v "127.0.0."` untuk menampilkan daftar yang tidak berjalan di localhost (127.0.0.1) dan tambahan perintah `grep -v tcp6` untuk menampilkan daftar yang tidak berjalan di IPv6 sehingga hanya IPv4. Terakhir kita menghitung program yang berstatus `LISTEN` menggunakan perintah `grep -c LISTEN`   
```sh
netstat -tlpn | grep -v "127.0.0." | grep -v tcp6 | grep -c LISTEN
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2021.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2022.JPG)

- **Answer**
```sh
7
```

- **Question:** Determine what user the ProFTPd server is running under. Submit the username as the answer.
- Gunakan perintah `ps -aux` untuk menampilkan semua daftar proses yang berjalan di mesin kemudian filter daftar yang mengandung `proftpd`
```sh
ps -aux | grep proftpd
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2023.JPG)

- **Answer**
```sh
proftpd
```

- **Question:** Use cURL from your Pwnbox (not the target machine) to obtain the source code of the `https://www.inlanefreight.com` website and filter all unique paths of that domain. Submit the number of these paths as the answer. 
- Buka terminal baru dan jalankan perintah berikut ini. Perintah `sort -u` digunakan mengurutkan hasil pencarian yang unique
```sh
curl https://www.inlanefreight.com/ | grep -Po "https://www.inlanefreight.com/[^'\"]*" | sort -u | wc -l
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2024.JPG)

- **Answer**
```sh
34
```

## User Management
- **Question:** Which option needs to be set to create a home directory for a new user using "useradd" command? 
- Tambahkan opsi `--help` pada perintah `useradd` untuk melihat daftar opsi yang tersedia
```sh
useradd --help
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2025.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2026.JPG)

- **Answer**
```sh
-m
```

- **Question:** Which option needs to be set to lock a user account using the "usermod" command? (long version of the option)
- Tambahkan opsi `--help` pada perintah `usermod` untuk melihat daftar opsi yang tersedia
```sh
usermod --help
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2027.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2028.JPG)

- **Answer**
```sh
--lock
```

- **Question:** Which option needs to be set to execute a command as a different user using the "su" command? (long version of the option)
- Tambahkan opsi `--help` pada perintah `su` untuk melihat daftar opsi yang tersedia
```sh
su --help
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2029.JPG)

- **Answer**
```sh
--command
```

## Service and Process Management
- **Question:** Use the "systemctl" command to list all units of services and submit the unit name with the description "Load AppArmor profiles managed internally by snapd" as the answer. 
```sh
systemctl | grep "Load AppArmor profiles managed internally by snapd"
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2030.JPG)

- **Answer**
```sh
snapd.apparmor.service
```

## Task Scheduling
- **Question:** What is the Type of the service of the "syslog.service"?
```sh
systemctl show syslog.service
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2031.JPG)

- **Answer**
```sh
notify
```

## Working with Web Services
- **Question:** Find a way to start a simple HTTP server inside Pwnbox or your local VM using "npm". Submit the command that starts the web server on port 8080 (use the short argument to specify the port number).
- **Answer**
```sh
http-server -p 8080
```

- **Question:** Find a way to start a simple HTTP server inside Pwnbox or your local VM using "php". Submit the command that starts the web server on the localhost (127.0.0.1) on port 8080. 
- **Answer**
```sh
php -S 127.0.0.1:8080
```

## File System Management
- **Question:** How many partitions exist in our Pwnbox? (Format: 0)
```sh
lsblk
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Linux%20fundamentals/assets/linux%20fundamental%2032.JPG)

- **Answer**
```sh
3
```