# Introduction to Web Applications
- Link modul: https://academy.hackthebox.com/module/details/75

## HTML
- **Question:**  What is the HTML tag used to show an image?
- Tag HTML yang digunakan untuk menampilkan gambar adalah `<img>`. Format penulisan tag `<img>` adalah sebagai berikut
```sh
<img src="path_gambar" alt="caption" width="panjang" height="lebar">
```
- **Answer:**
```sh
<img>
```

## Cascading Style Sheets (CSS)
- **Question:** What is the CSS "property: value" used to make an HTML element's text aligned to the left?
- Property CSS untuk mengatur posisi tampilan text adalah `text-align`. Property `text-align` mempunyai syntax dan nilai property sebagai berikut:
```sh
text-align: left|right|center|justify|initial|inherit;
```
- **Answer:**
```sh
text-align: left;
```

## Sensitive Data Exposure
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%202.JPG)

- **Question:** Check the above login form for exposed passwords. Submit the password as the answer.
- Akses web di browser

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%203.JPG)

- Tekan `Ctrl+U` untuk membuka source code halaman. Pada source code halaman ditemukan informasi kredensial untuk mengakses login

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%204.JPG)

- **Answer:**
```sh
HiddenInPlainSight
```

## HTML Injection
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%205.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%206.JPG)

- **Question:** What text would be displayed on the page if we use the following payload as our input: <a href="http://www.hackthebox.com">Click Me</a>
- Akses web di browser dan klik tombol di halaman tersebut

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%207.JPG)

- Setelah muncul pop up, masukkan payload diatas lalu tekan tombol **OK**
```sh
<a href="http://www.hackthebox.com">Click Me</a>
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%208.JPG)

- Setelah berhasil diinput akan muncul tampilan sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%209.JPG)

- **Answer:**
```sh
Your name is Click Me
```

## Cross-Site Scripting (XSS)
- **Question:** Try to use XSS to get the cookie value in the above page
- Akses halaman web di section sebelumnya lalu klik tombol **Click to enter your name**

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%2010.JPG)

- Setelah muncul pop up, masukkan payload XSS sebagai berikut lalu tekan tombol **OK**
```sh
<img src=/ onerror=alert(document.cookie)>
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%2011.JPG)

- Setelah berhasil diinput akan muncul pop up yang menampilkan cookie halaman yang menandakan bahwa halaman web tersebut rentan terhadap XSS

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%2012.JPG)

- **Answer:**
```sh
XSSisFun
```

## Back End Servers
- **Question:** What operating system is 'WAMP' used with? 
- WAMP adalah singkatan dari Windows, Apache, MySQL, dan PHP. Jadi WAMP berjalan di platform Windows
- **Answer:**
```sh
Windows
```

## Web Servers
- **Question:** If a web server returns an HTTP code 201, what does it stand for?
- HTTP code 201 berarti `Created` yang menandakan bahwa request berhasil dilakukan dan berhasil membuat sumber data atau resource baru 
- **Answer:**
```sh
Created
```

## Databases
- **Question:** What type of database is Google's Firebase Database?
- Firebase adalah database NoSQL yang dihosting di cloud yang memungkinkan organisasi menyimpan dan menyinkronkan data secara real-time di semua perangkat penggunanya (referensi: https://www.techtarget.com/searchmobilecomputing/definition/Google-Firebase#:~:text=The%20Firebase%20Realtime%20Database%20is,all%20of%20their%20users'%20devices. )
- **Answer:**
```sh
NoSQL
```

## Development Frameworks & APIs
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%2013.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%2014.JPG)

- **Question:** Use GET request '/index.php?id=0' to search for the name of the user with id number 1?
- Akses halaman web dengan URL sebagai berikut
```sh
http://ip:port/index.php?id=0
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%2015.JPG)

- Pada parameter `id=0` tidak ditemukan data namun setelah diubah nilainya menjadi 1 kita berhasil mendapatkan nama user

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%2016.JPG)

- **Answer:**
```sh
superadmin
```

## Common Web Vulnerabilities
- **Question:** To which of the above categories does public vulnerability 'CVE-2014-6271' belongs to?
- Celah CVE-2014-6271 disebut juga `ShellShock` dimana penyerang dapat mengeksekusi kode dari jarak jauh melalui fitur ForceCommand di OpenSSH sshd, modul mod_cgi dan mod_cgid di Apache HTTP Server (referensi: https://nvd.nist.gov/vuln/detail/cve-2014-6271 )
- **Answer:**
```sh
Command Injection
```

## Public Vulnerabilities
- **Question:** What is the CVSS score of the public vulnerability CVE-2017-0144?
- CVSS calculator versi 2 dapat diakses di link https://nvd.nist.gov/vuln-metrics/cvss/v2-calculator 
- Untuk mempersingkat waktu anda dapat langsung mengakses link https://nvd.nist.gov/vuln/search untuk mengetahui CVSS score dari celah keamanan CVE-2017-0144. Pada field pencarian ketikkan CVE yang akan dicari dan tekan tombol **Search**

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%2017.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Introduction%20to%20Web%20Applications/assets/intro%20web%2018.JPG)

- **Answer:**
```sh
9.3
```