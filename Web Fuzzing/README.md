# Web Fuzzing
- Link modul: https://academy.hackthebox.com/module/details/280
- Pada modul ini kita akan menggunakan wordlists dari seclists. Wordlists ini secara default belum tersedia di kali linux, jadi anda perlu menginstalasi terlebih dahulu dengan perintah sebagai berikut
```sh
sudo apt install seclists
```

## Directory and File Fuzzing
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%202.JPG)

- **Question:** Within the "webfuzzing_hidden_path" path on the target system (ie http://IP:PORT/webfuzzing_hidden_path/), fuzz for folders and then files to find the flag.
- Jalankan tool `ffuf` untuk menemukan direktori web tersembunyi
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://ip:port/webfuzzing_hidden_path/FUZZ -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%203.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%204.JPG)

- Setelah perintah diatas jalankan, ditemukan halaman `/flag` pada web. Selanjutnya kita lakukan pengecekan di browser dengan URL `http://ip:port/webfuzzing_hidden_path/flag`. Halaman `/flag` ternyata masih web direktori sehingga kita perlu menjalankan tool `ffuf` kembali untuk menemukan web path berikutnya

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%205.JPG)

- Jalankan tool `ffuf` untuk menemukan halaman web tersembunyi setelah path `/flag/`
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://ip:port/webfuzzing_hidden_path/flag/FUZZ -c -ic -e .html,.php,.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%206.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%207.JPG)

- Setelah perintah diatas jalankan, ditemukan halaman `flag.html`. Selanjutnya kita buka halaman tersebut dibrowser dengan URL `http://ip:port/webfuzzing_hidden_path/flag/flag.html`. Setelah dibuka halaman tersebut berisi flag

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%208.JPG)

- **Answer:**
```sh
HTB{w3b_f1l3_fuzz1ng_fl4g}
```

## Recursive Fuzzing
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%209.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2010.JPG)

- **Question:** Recursively fuzz the "recursive_fuzz" path on the target system (ie http://IP:PORT/recursive_fuzz/) to find the flag.
- Jalankan tool `ffuf` untuk menemukan direktori web tersembunyi
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://ip:port/recursive_fuzz/FUZZ -c -ic -e .html -recursion -recursion-depth 2 -fc 403
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2011.JPG)

- Pada tahap pertama ditemukan path `/level1`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2012.JPG)

- Pada tahap berikutnya ditemukan path `/level2` sehingga URL yang didapat adalah `http://ip:port/recursive_fuzz/level1/level2`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2013.JPG)

- Setiap tahap pada proses diatas memerlukan waktu kurang lebih 36 menit sedangkan web hanya berjalan dalam waktu 90 menit sehingga kita kehabisan waktu dan perlu menghidupkan ulang web target. Setelah web target dihidupkan ulang, IP dan port mungkin berbeda dari sebelumnya sehingga anda perlu menggantinya

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2014.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2015.JPG)

- Jalankan tool `ffuf` untuk menemukan direktori web tersembunyi `/level1/level2/`
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://ip:port/recursive_fuzz/level1/level2/FUZZ -c -ic -e .html -fc 403 -recursion -recursion-depth 2
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2016.JPG)

- Pada tahap pertama ditemukan path `/level3`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2017.JPG)

- Pada tahap berikutnya ditemukan path `/threatcon_level2` sehingga URL yang didapat adalah `http://ip:port/recursive_fuzz/level1/level2/level3/threatcon_level2`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2018.JPG)

- Setelah dilakukan pengecekan di browser URL diatas berisi flag

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2019.JPG)

- **Answer:**
```sh
HTB{d33p3r_d1rector1es_ar3_c00l}
```

## Parameter and Value Fuzzing
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2020.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2021.JPG)

- **Question:** What flag do you find when successfully fuzzing the GET parameter?
- Akses halaman `/get.php` menggunakan tool `curl`. Setelah diakses muncul pesan bahwa halaman tersebut harus diakses dengan nama parameter `x`
```sh
curl http://ip:port/get.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2022.JPG)

- Sekarang kita tambahkan parameter `x` dengan nilai `1` pada URL. Setelah diakses muncul pesan bahwa nilai parameter tersebut invalid
```sh
curl http://ip:port/get.php?x=1
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2023.JPG)

- Selanjutnya kita coba jalankan tool `ffuf` untuk menemukan nilai parameter `x` yang sesuai
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://ip:port/get.php?x=FUZZ -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2024.JPG)

- Setelah dijalankan kita menemukan nilai parameter yang sesuai yaitu `OA_HTML` sehingga kita berhasil menemukan URL `http://ip:port/get.php?x=OA_HTML`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2025.JPG)

- Sekarang kita coba akses URL tersebut di browser dan kita berhasil menemukan flag

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2026.JPG)

- **Answer:**
```sh
HTB{g3t_fuzz1ng_succ3ss}
```

- **Question:** What flag do you find when successfully fuzzing the POST parameter?
- Akses halaman `/post.php` menggunakan tool `curl`. Setelah diakses muncul pesan bahwa halaman tersebut harus diakses dengan nama parameter `y`
```sh
curl -d "" http://ip:port/post.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2027.JPG)

- Selanjutnya kita coba jalankan tool `ffuf` untuk menemukan nilai parameter `y` yang sesuai
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://ip:port/post.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "y=FUZZ" -c -ic -mc 200
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2028.JPG)

- Setelah dijalankan kita menemukan nilai parameter yang sesuai yaitu `SUNWmc`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2029.JPG)

- Sekarang kita coba post data tersebut menggunakan tool `curl`
```sh
curl -d "y=SUNWmc" http://ip:port/post.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2030.JPG)

- **Answer:**
```sh
HTB{p0st_fuzz1ng_succ3ss}
```

## Virtual Host and Subdomain Fuzzing
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2031.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2032.JPG)

- **Question:** Using GoBuster against the target system to fuzz for vhosts using the common.txt wordlist, which vhost starts with the prefix "web-"? Respond with the full vhost, eg web-123.inlanefreight.htb.
- Pada percobaan kali ini, kita akan menggunakan tool `gobuster`. Tool ini secara default belum tersedia di kali linux sehingga anda perlu menginstalasi terlebih dahulu dengan perintah sebagai berikut
```sh
sudo apt install gobuster
```
- Tambahkan IP ke file `/etc/hosts` terlebih dahulu
```sh
echo "ip inlanefreight.htb" | sudo tee -a /etc/hosts
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2033.JPG)

- Jalankan tool `gobuster` untuk menemukan vhost
```sh
gobuster vhost -u http://inlanefreight.htb:port -w /usr/share/seclists/Discovery/Web-Content/common.txt --append-domain
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2034.JPG)

- **Answer:**
```sh
web-beans.inlanefreight.htb
```

- **Question:** Using GoBuster against inlanefreight.com to fuzz for subdomains using the subdomains-top1million-5000.txt wordlist, which subdomain starts with the prefix "su"? Respond with the full vhost, eg web.inlanefreight.com.
- Jalankan tool `gobuster` untuk menemukan subdomain
```sh
gobuster dns -d inlanefreight.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2035.JPG)

- **Answer:**
```sh
support.inlanefreight.com
```

## Filtering Fuzzing Output
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2036.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2037.JPG)

- **Question:** What flag do you find when successfully fuzzing the POST parameter?
- Akses halaman `/post.php` menggunakan tool `curl`. Setelah diakses muncul pesan bahwa halaman tersebut harus diakses dengan nama parameter `y`
```sh
curl -d "" http://ip:port/post.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2038.JPG)

- Selanjutnya kita coba jalankan tool `ffuf` untuk menemukan nilai parameter `y` yang sesuai
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://ip:port/post.php -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "y=FUZZ" -fc 403 -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2039.JPG)

- Setelah dijalankan kita menemukan nilai parameter yang sesuai yaitu `SUNWmc`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2040.JPG)

- Sekarang kita coba post data tersebut menggunakan tool `curl`
```sh
curl -d "y=SUNWmc" http://ip:port/post.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2041.JPG)

- **Answer:**
```sh
HTB{p0st_fuzz1ng_succ3ss}
```

## Validating Findings
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2042.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2043.JPG)

- **Question:** Fuzz the target system using directory-list-2.3-medium.txt, looking for a hidden directory. Once you have found the hidden directory, responsibly determine the validity of the vulnerability by analyzing the tar.gz file in the directory. Answer using the full Content-Length header, eg "Content-Length: 1337"
- Jalankan tool `gobuster` untuk menemukan halaman tersembunyi
```sh
gobuster dir -u http://ip:port/ -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2044.JPG)

- Ditemukan halaman `/ur-hiddenmember` pada hasil pencarian diatas. Setelah dicek di browser dihalaman tersebut terdapat file `backup.tar.gz` sehingga kita tidak perlu melanjutkan proses pencarian pada tool `gobuster`. Tekan `Ctrl+C` untuk menghentikan prosesnya

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2045.JPG)

- Lakukan pengecekan dengan tool `curl`
```sh
curl -I http://ip:port/ur-hiddenmember/backup.tar.gz
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2046.JPG)

- **Answer:**
```sh
Content-Length: 210
```

## API Fuzzing
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2047.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2048.JPG)

- **Question:** What is the value returned by the endpoint that the api fuzzer has identified?
- Install tool [webfuzz_api](https://github.com/PandaSt0rm/webfuzz_api) terlebih dahulu
```sh
git clone https://github.com/PandaSt0rm/webfuzz_api.git
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2049.JPG)

- Install depedensi tool `webfuzz_api`
```sh
cd webfuzz_api
pip3 install -r requirements.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2050.JPG)

- Jalankan program `api_fuzzer.py` untuk menemukan endpoint API dan tunggu hingga proses selesai
```sh
python3 api_fuzzer.py http://ip:port
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2051.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2052.JPG)

- Dari hasil tool diatas ditemukan endpoint `/czcmdcvt`. Sekarang kita akses endpoint tersebut menggunakan tool `curl` untuk mendapatkan flag
```sh
curl http://ip:port/czcmdcvt
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2053.JPG)

- **Answer:**
```sh
h1dd3n_r357
```

## Skills Assessment
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2054.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2055.JPG)

- **Question:** After completing all steps in the assessment, you will be presented with a page that contains a flag in the format of HTB{...}. What is that flag?
- Lakukan pencarian halaman tersembunyi dengan tool `gobuster`
```sh
gobuster dir -u http://ip:port/ -w /usr/share/seclists/Discovery/Web-Content/common.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2056.JPG)

- Pada percobaan pertama ditemukan direktori `/admin`. Sekarang kita coba cari halaman tersembunyi dibalik direktori `/admin` yang berekstensi `.php` dan `.html` dengan tool `gobuster`
```sh
gobuster dir -u http://ip:port/admin/ -w /usr/share/seclists/Discovery/Web-Content/common.txt -x .php,.html
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2057.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2058.JPG)

- Dari percobaan kedua ditemukan halaman `/panel.php`. Sekarang akses halaman tersebut menggunakan tool `curl` maka muncul pesan bahwa halaman tersebut harus diakses dengan paramaeter `accessID`
```sh
curl http://ip:port/admin/panel.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2059.JPG)

- Selanjutnya kita cari nilai parameter yang sesuai dengan tool `ffuf`. Pada percobaan pertama terlalu banyak temuan halaman dengan ukuran 58 sehingga kita melakukan percobaan ulang dengan filter ukuran 58
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://ip:port/admin/panel.php?accessID=FUZZ -c -ic -fs 58
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2060.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2061.JPG)

- Pada percobaan diatas ditemukan nilai parameter `getaccess`, selanjutnya kita coba akses menggunakan tool `curl`
```sh
curl http://ip:port/admin/panel.php?accessID=getaccess
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2062.JPG)

- Ditemukan petunjuk bahwa kita harus melakukan fuzzing vhost dengan nama domain `fuzzing_fun.htb` untuk itu kita perlu menambahkan IP web target ke file `/etc/hosts`
```sh
echo "ip fuzzing_fun.htb" | sudo tee -a /etc/hosts
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2063.JPG)

- Setelah berhasil ditambahkan, akses domain tersebut menggunakan tool `curl`
```sh
curl http://fuzzing_fun.htb:port
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2064.JPG)

- Ditemukan bahwa titik awal berada di folder `/godeep` namun kita perlu menemukan vhost yang lain sehingga kita gunakan tool `ffuf` untuk menemukan sub domain yang lain
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://fuzzing_fun.htb:port -H 'Host: FUZZ.fuzzing_fun.htb' -fc 403 -c -ic
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2065.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2066.JPG)

- Ditemukan sub domain `hidden` sehingga kita perlu menambahkan sub domain tersebut ke file `/etc/hosts`
```sh
echo "ip hidden.fuzzing_fun.htb" | sudo tee -a /etc/hosts
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2067.JPG)

- Berikut kita coba temukan folder web tersembunyi lainnya dibalik folder `/godeep` menggunakan domain `hidden.fuzzing_fun.htb` dengan tool `ffuf` secara rekursif agar dapat menemukan path secara keseluruhan
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://hidden.fuzzing_fun.htb:port/godeep/FUZZ -fc 403 -c -ic -recursion
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2068.JPG)

- Pada iterasi terakhir ditemukan path halaman `/godeep/stoneedge/bbclone/typo3/` lalu selanjutnya ditemukan halaman `index.php` sehingga secara keseluruhan URL nya adalah `http://hidden.fuzzing_fun.htb:port/godeep/stoneedge/bbclone/typo3/index.php`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2069.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2070.JPG)

- Akses halaman tersebut menggunakan tool `curl`
```sh
curl http://hidden.fuzzing_fun.htb:port/godeep/stoneedge/bbclone/typo3/index.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20Fuzzing/assets/web%20fuzzing%2071.JPG)

- **Answer:**
```sh
HTB{w3b_fuzz1ng_sk1lls}
```