# Attacking Web Applications with Ffuf
- Link modul: https://academy.hackthebox.com/module/details/54
- Pada modul ini kita akan menggunakan wordlists dari seclists. Wordlists ini secara default belum tersedia di kali linux, jadi anda perlu menginstalasi terlebih dahulu dengan perintah sebagai berikut
```sh
sudo apt install seclists
```

## Directory Fuzzing
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%202.JPG)

- **Question:** In addition to the directory we found above, there is another directory that can be found. What is it?
- Jalankan tool `ffuf` untuk menemukan direktori web tersembunyi
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt -u http://ip:port/FUZZ -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%203.JPG)

- Ditemukan halaman `/forum` pada hasil pencarian diatas

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%204.JPG)

- **Answer:**
```sh
forum
```

## Page Fuzzing
- **Question:** Try to use what you learned in this section to fuzz the '/blog' directory and find all pages. One of them should contain a flag. What is the flag?
- Jalankan tool `ffuf` untuk menemukan halaman web tersembunyi
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://ip:port/blog/FUZZ.php -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%205.JPG)

- Ditemukan halaman `/home.php` pada hasil pencarian diatas

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%206.JPG)

- Sekarang kita buka halaman diatas di browser

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%207.JPG)

- **Answer:**
```sh
HTB{***}
```

## Recursive Fuzzing
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%208.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%209.JPG)

- **Question:** Try to repeat what you learned so far to find more files/directories. One of them should give you a flag. What is the content of the flag?
- Tambahkan IP ke file `/etc/hosts`
```sh
echo "ip fuzzing_fun.htb" | sudo tee -a /etc/hosts
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2010.JPG)

- Jalankan tool `ffuf` untuk menemukan halaman web tersembunyi
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://academy.htb:port/FUZZ -c -ic -recursion -e .php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2011.JPG)

- Ditemukan direktori `/forum` dan selanjutnya ditemukan halaman `flag.php`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2012.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2013.JPG)

- Sekarang kita coba akses URL `http://academy.htb:port/forum/flag.php` via browser

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2014.JPG)

- **Answer:**
```sh
HTB{***}
```

## Sub-domain Fuzzing
- **Question:** Try running a sub-domain fuzzing test on 'inlanefreight.com' to find a customer sub-domain portal. What is the full domain of it?
- Jalankan tool `ffuf` untuk menemukan sub domain
```sh
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u https://FUZZ.inlanefreight.com/ -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2015.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2016.JPG)

- **Answer:**
```sh
customer.inlanefreight.com
```

## Filtering Results
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2017.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2018.JPG)

- **Question:** Try running a VHost fuzzing scan on 'academy.htb', and see what other VHosts you get. What other VHosts did you get?
- Tambahkan IP ke file `/etc/hosts` terlebih dahulu
```sh
echo "ip academy.htb" | sudo tee -a /etc/hosts
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2019.JPG)

- Pada percobaan pertama dengan tool `ffuf` banyak ditemukan vhost dengan size 986 sehingga kita perlu filter untuk halaman yang berukuran 986 dengan perintah sebagai berikut
```sh
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:port/ -H 'Host: FUZZ.academy.htb' -c -ic -fc 403 -fs 986
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2020.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2021.JPG)

- **Answer:**
```sh
test.academy.htb
```

## Parameter Fuzzing - GET
- **Question:** Using what you learned in this section, run a parameter fuzzing scan on this page. what is the parameter accepted by this webpage?
- Tambahkan VHost `admin.academy.htb` ke file `/etc/hosts` terlebih dahulu
```sh
echo "ip admin.academy.htb" | sudo tee -a /etc/hosts
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2022.JPG)

- Jalankan tool `ffuf` untuk menemukan nama parameter yang sesuai. Pada percobaan pertama ditemukan banyak hasil dengan ukuran halaman 798 sehingga kita filter untuk halaman yang berukuran 798
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:port/admin/admin.php?FUZZ=key -c -ic -fs 798
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2023.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2024.JPG)

- **Answer:**
```sh
user
```

## Value Fuzzing
- **Question:** Try to create the 'ids.txt' wordlist, identify the accepted value with a fuzzing scan, and then use it in a 'POST' request with 'curl' to collect the flag. What is the content of the flag?
- Buat file `ids.txt` dengan bash script terlebih dahulu
```sh
for i in $(seq 1 1000); do echo $i >> ids.txt; done
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2025.JPG)

- Jalankan tool `ffuf` untuk menemukan id yang sesuai. Pada percobaan pertama ditemukan banyak hasil dengan ukuran halaman 768 sehingga kita filter untuk halaman yang berukuran 768
```sh
ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:port/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -c -ic -fs 768
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2026.JPG)

- Nilai id yang sesuai adalah 73

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2027.JPG)

- Sekarang kita akses halaman `/admin/admin.php` menggunakan tool `curl` dengan menambahkan parameter id dengan nilai 73
```sh
curl -d "id=73" http://admin.academy.htb:port/admin/admin.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2028.JPG)

- **Answer:**
```sh
HTB{***}
```

## Skills Assessment - Web Fuzzing
- Jika di task sebelumnya sudah tersimpan domain `academy.htb` dan `admin.academy.htb` di file `/etc/hosts` maka anda perlu menghapusnya terlebih dahulu sebelum memulai task ini
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2029.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2030.JPG)

- **Question:** Run a sub-domain/vhost fuzzing scan on `*.academy.htb` for the IP shown above. What are all the sub-domains you can identify? (Only write the sub-domain name)
- Tambahkan ip ke file `/etc/hosts`
```sh
echo "ip academy.htb" | sudo tee -a /etc/hosts
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2031.JPG)

- Temukan sub-domain/vhost dengan tool `ffuf`. Pada percobaan pertama ditemukan banyak hasil dengan ukuran halaman 985 sehingga kita filter untuk halaman yang berukuran 985
```sh
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:port/ -H 'Host: FUZZ.academy.htb' -c -ic -fc 403 -fs 985
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2032.JPG)

- Ditemukan 3 vhost dari hasil pencarian

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2033.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2034.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2035.JPG)

- **Answer:**
```sh
archive, test, faculty
```

- **Question:** Before you run your page fuzzing scan, you should first run an extension fuzzing scan. What are the different extensions accepted by the domains?
- Tambahkan vhost diatas ke file `/etc/hosts`
```sh
echo "ip archive.academy.htb test.academy.htb faculty.academy.htb" | sudo tee -a /etc/hosts
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2036.JPG)

- Temukan ekstensi halaman `index` di masing-masing vhost
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://archive.academy.htb:port/indexFUZZ -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2037.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2038.JPG)

```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://test.academy.htb:port/indexFUZZ -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2039.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2040.JPG)

```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://faculty.academy.htb:port/indexFUZZ -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2041.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2042.JPG)

- **Answer:**
```sh
.php, .phps, .php7
```

- **Question:** One of the pages you will identify should say 'You don't have access!'. What is the full page URL?
- Tahap ini memerlukan waktu yang cukup lama, mungkin saja anda perlu merefresh kembali web target. Jika web target sudah direfresh, anda perlu mengganti IP vhost pada file `/etc/hosts` seperti pada langkah diatas 
- Lakukan recursif fuzzing pada setiap vhost diatas
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://archive.academy.htb:port/FUZZ -recursion -e .php,.phps -c -ic -fc 403 -v
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2043.JPG)

- Tidak ditemukan halaman yang valid dari hasil fuzzing diatas

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2044.JPG)

```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://test.academy.htb:port/FUZZ -recursion -e .php,.phps -c -ic -fc 403 -v
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2045.JPG)

- Hingga proses selesai, tidak ditemukan page apapun

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2046.JPG)

```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://faculty.academy.htb:port/FUZZ -recursion -e .php,.phps,.php7 -c -ic -fc 403 -v
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2047.JPG)

- Ditemukan halaman `/courses/linux-security.php7` pada hasil fuzzing diatas

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2048.JPG)

- Jika kita cek di browser halaman diatas berisi tampilan sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2049.JPG)

- **Answer:**
```sh
http://faculty.academy.htb:PORT/courses/linux-security.php7
```

- **Question:**  In the page from the previous question, you should be able to find multiple parameters that are accepted by the page. What are they?
- Lakukan fuzzing untuk mendapatkan nama parameter dengan method GET. Pada percobaan pertama ditemukan banyak hasil dengan ukuran halaman 774 sehingga kita filter untuk halaman yang berukuran 774
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://faculty.academy.htb:port/courses/linux-security.php7?FUZZ=key -c -ic -fs 774
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2050.JPG)

- Ditemukan nama parameter `user` dari hasil fuzzing diatas

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2051.JPG)

- Lakukan fuzzing untuk mendapatkan nama parameter dengan method POST
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -u http://faculty.academy.htb:port/courses/linux-security.php7 -c -ic -fs 774
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2052.JPG)

- Ditemukan nama parameter `user` dan `username` dari hasil fuzzing diatas

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2053.JPG)

- **Answer:**
```sh
user, username
```

- **Question:** Try fuzzing the parameters you identified for working values. One of them should return a flag. What is the content of the flag?
- Untuk daftar username kita akan gunakan wordlists `Usernames/Names/names.txt` dari seclists
- Lakukan fuzzing untuk menemukan nilai parameter yang cocok. Pada percobaan pertama ditemukan banyak hasil dengan ukuran halaman 781 sehingga kita filter untuk halaman yang berukuran 781
```sh
ffuf -w /usr/share/seclists/Usernames/Names/names.txt:FUZZ -X POST -d 'username=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -u http://faculty.academy.htb:port/courses/linux-security.php7 -c -ic -fs 781
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2054.JPG)

- Username yang cocok adalah `harry`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2055.JPG)

- Lakukan post data menggunakan tool `curl`
```sh
curl -d "username=harry" -X POST http://faculty.academy.htb:port/courses/linux-security.php7
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Attacking%20Web%20Applications%20with%20Ffuf/assets/ffuf%2056.JPG)

- **Answer:**
```sh
HTB{***}
```