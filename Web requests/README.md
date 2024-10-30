# Web Requests
- Link modul: https://academy.hackthebox.com/module/details/35

## HyperText Transfer Protocol (HTTP)
- Jalankan web target terlebih dahulu

- **Question:** To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above. 
- Buka terminal dan unduh halaman `download.php` menggunakan curl
```sh
curl -O http://ip:port/download.php
```

- Baca isi file `download.php` di terminal
```sh
cat download.php
```

- **Answer:**
```sh
HTB{64$!c_cURL_u$3r}
```

## HTTP Requests and Responses
- **Question:** What is the HTTP method used while intercepting the request? (case-sensitive)
```sh
curl http://ip:port/ -v
```

- **Answer:**
```sh
GET
```

- **Question:** Send a GET request to the above server, and read the response headers to find the version of Apache running on the server, then submit it as the answer. (answer format: X.Y.ZZ)
- Secara default curl akan mengirimkan request `GET`
```sh
curl http://ip:port/ -v
```

- **Answer:**
```sh
2.4.41
```

## HTTP Headers
- Jalankan web target terlebih dahulu

- **Question:** he server above loads the flag after the page is loaded. Use the Network tab in the browser devtools to see what requests are made by the page, and find the request to the flag.
- Buka halaman web di browser dengan URL `http://ip:port`

- Klik kanan pada halaman web lalu pilih **Inspect**

- Klik tab Network

- Reload halaman web tersebut, maka akan tampil beberapa request di tab Network

- Pada tab Network terdapat request yang mengarah ke direktori `flag_hash.txt` klik request tersebut

- Pindah ke tab Response maka akan terdapat flag disana

- **Answer:**
```sh
HTB{p493_r3qu3$t$_m0n!t0r}
```

## GET
- Jalankan web target terlebih dahulu

- **Question:** The exercise above seems to be broken, as it returns incorrect results. Use the browser devtools to see what is the request it is sending when we search, and use cURL to search for 'flag' and obtain the flag.

- Buka halaman web di browser dengan URL `http://ip:port` setelah itu masukkan username dan password yang sudah tersedia di soal


- Klik kanan pada halaman web lalu pilih **Inspect**

- Klik tab Network

- Ketik kata pencarian `flag` pada field pencarian lalu tekan enter

- Pada tab Network terdapat request yang mengarah ke direktori `/search.php?search=flag` yang di responsenya terdapat pesan bahwa URL ini harus diakses menggunakan curl

- Sekarang kita akses halaman tersebut menggunakan curl
```sh
curl http://ip:port/search.php?search=flag -u admin:admin
```


- **Answer:**
```sh
HTB{curl_g3773r}
```

## POST
- Jalankan web target terlebih dahulu

- **Question:** Obtain a session cookie through a valid login, and then use the cookie with cURL to search for the flag through a JSON POST request to '/search.php'

- Buka halaman web di browser dengan URL `http://ip:port` setelah itu masukkan username dan password yang sudah tersedia di soal

- Klik kanan pada halaman web lalu pilih **Inspect**

- Klik tab **Storage** untuk mendapatkan nama cookie dan nilai cookie

- Klik tab Network

- Ketik kata pencarian `flag` pada field pencarian lalu tekan enter

- Pada tab Network terdapat request yang mengarah ke direktori `/search.php` dengan method `POST` dan pada tab Request terdapat parameter `search` dengan struktur JSON


- Sekarang kita lakukan request `POST` ke halaman tersebut menggunakan curl
```sh
curl -X POST -b 'PHPSESSID=cookie' -H 'Content-Type:application/json' -d '{"search":"flag"}' http://ip:port/search.php
```


- **Answer:**
```sh
HTB{p0$t_r3p34t3r}
```