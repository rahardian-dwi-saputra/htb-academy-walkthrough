# Web Requests
- Link modul: https://academy.hackthebox.com/module/details/35

## HyperText Transfer Protocol (HTTP)
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%201.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%202.JPG)

- **Question:** To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above. 
- Buka terminal dan unduh halaman `download.php` menggunakan curl
```sh
curl -O http://ip:port/download.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%203.JPG)

- Baca isi file `download.php` di terminal
```sh
cat download.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%204.JPG)

- **Answer:**
```sh
HTB{64$!c_cURL_u$3r}
```

## HTTP Requests and Responses
- **Question:** What is the HTTP method used while intercepting the request? (case-sensitive)
```sh
curl http://ip:port/ -v
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%205.JPG)

- **Answer:**
```sh
GET
```

- **Question:** Send a GET request to the above server, and read the response headers to find the version of Apache running on the server, then submit it as the answer. (answer format: X.Y.ZZ)
- Secara default curl akan mengirimkan request `GET`
```sh
curl http://ip:port/ -v
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%206.JPG)

- **Answer:**
```sh
2.4.41
```

## HTTP Headers
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%207.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%208.JPG)

- **Question:** he server above loads the flag after the page is loaded. Use the Network tab in the browser devtools to see what requests are made by the page, and find the request to the flag.
- Buka halaman web di browser dengan URL `http://ip:port`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%209.JPG)

- Klik kanan pada halaman web lalu pilih **Inspect**

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2010.JPG)

- Klik tab Network

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2011.JPG)

- Reload halaman web tersebut, maka akan tampil beberapa request di tab Network

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2012.JPG)

- Pada tab Network terdapat request yang mengarah ke direktori `flag_hash.txt` klik request tersebut

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2013.JPG)

- Pindah ke tab Response maka akan terdapat flag disana

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2014.JPG)

- **Answer:**
```sh
HTB{p493_r3qu3$t$_m0n!t0r}
```

## GET
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2015.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2016.JPG)

- **Question:** The exercise above seems to be broken, as it returns incorrect results. Use the browser devtools to see what is the request it is sending when we search, and use cURL to search for 'flag' and obtain the flag.
- Buka halaman web di browser dengan URL `http://ip:port` setelah itu masukkan username dan password yang sudah tersedia di soal

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2017.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2018.JPG)

- Klik kanan pada halaman web lalu pilih **Inspect**

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2019.JPG)

- Klik tab Network

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2020.JPG)

- Ketik kata pencarian `flag` pada field pencarian lalu tekan enter

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2021.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2022.JPG)

- Pada tab Network terdapat request yang mengarah ke direktori `/search.php?search=flag` yang di responsenya terdapat pesan bahwa URL ini harus diakses menggunakan curl

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2023.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2024.JPG)

- Sekarang kita akses halaman tersebut menggunakan curl
```sh
curl http://ip:port/search.php?search=flag -u admin:admin
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2025.JPG)

- **Answer:**
```sh
HTB{curl_g3773r}
```

## POST
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2026.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2027.JPG)

- **Question:** Obtain a session cookie through a valid login, and then use the cookie with cURL to search for the flag through a JSON POST request to '/search.php'
- Buka halaman web di browser dengan URL `http://ip:port` setelah itu masukkan username dan password yang sudah tersedia di soal

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2028.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2029.JPG)

- Klik kanan pada halaman web lalu pilih **Inspect**

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2030.JPG)

- Klik tab **Storage** untuk mendapatkan nama cookie dan nilai cookie

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2031.JPG)

- Klik tab Network

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2032.JPG)

- Ketik kata pencarian `flag` pada field pencarian lalu tekan enter

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2033.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2034.JPG)

- Pada tab Network terdapat request yang mengarah ke direktori `/search.php` dengan method `POST` dan pada tab Request terdapat parameter `search` dengan struktur JSON

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2035.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2036.JPG)

- Sekarang kita lakukan request `POST` ke halaman tersebut menggunakan curl
```sh
curl -X POST -b 'PHPSESSID=cookie' -H 'Content-Type:application/json' -d '{"search":"flag"}' http://ip:port/search.php
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2037.JPG)

- **Answer:**
```sh
HTB{p0$t_r3p34t3r}
```

## CRUD API
- Jalankan web target terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2038.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2039.JPG)

- **Question:** First, try to update any city's name to be 'flag'. Then, delete any city. Once done, search for a city named 'flag' to get the flag.
- Install jq jika belum terinstall
```sh
sudo apt install jq
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2040.JPG)

- Akses endpoint `/city` untuk mendapatkan daftar seluruh kota
```sh
curl -s http://ip:port/api.php/city | jq
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2041.JPG)

- Tambahkan parameter nama kota untuk mencari nama kota tertentu
```sh
curl -s http://ip:port/api.php/city/{city_name} | jq
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2042.JPG)

- Sekarang kita ubah nama salah satu kota, misalnya `London` menjadi `flag`
```sh
curl -X PUT -d '{"city_name":"flag"}' http://ip:port/api.php/city/{city_name}
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2043.JPG)

- Untuk pengecekan kita bisa akses endpoint `/city` untuk memastikan nama kota `London` menjadi `flag`

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2044.JPG)

- Sekarang kita coba hapus salah satu nama kota, misalnya nama kota `Leeds`
```sh
curl -X DELETE http://ip:port/api.php/city/leeds
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2045.JPG)

- Untuk pengecekan kita bisa melakukan pencarian data dengan nama kota `Leeds`. Jika datanya kosong maka data tersebut berhasil dihapus

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2046.JPG)

- Sekarang kita melakukan pencarian data dengan nama kota `flag` untuk mendapatkan flag
```sh
curl -s http://ip:port/api.php/city/flag | jq
```

![alt text](https://github.com/rahardian-dwi-saputra/htb-academy-walkthrough/blob/main/Web%20requests/assets/web%20request%2047.JPG)

- **Answer:**
```sh
HTB{crud_4p!_m4n!pul4t0r}
```