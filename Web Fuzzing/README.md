# Web Fuzzing
- Link modul: https://academy.hackthebox.com/module/details/280
- Pada modul ini kita akan menggunakan wordlists dari seclists. Wordlists ini secara default belum tersedia di kali linux, jadi anda perlu menginstalasi terlebih dahulu dengan perintah sebagai berikut
```sh
sudo apt install seclists
```

## Directory and File Fuzzing
- Jalankan web target terlebih dahulu
- **Question:** Within the "webfuzzing_hidden_path" path on the target system (ie http://IP:PORT/webfuzzing_hidden_path/), fuzz for folders and then files to find the flag.

- Jalankan tool `ffuf` untuk menemukan direktori web tersembunyi
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://ip:port/webfuzzing_hidden_path/FUZZ -c -ic
```

- Setelah perintah diatas jalankan, ditemukan halaman `/flag` pada web. Selanjutnya kita lakukan pengecekan di browser dengan URL `http://ip:port/webfuzzing_hidden_path/flag`. Halaman `/flag` ternyata masih web direktori sehingga kita perlu menjalankan tool `ffuf` kembali untuk menemukan web path berikutnya



- Jalankan tool `ffuf` untuk menemukan halaman web tersembunyi setelah path `/flag/`
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://ip:port/webfuzzing_hidden_path/flag/FUZZ -c -ic -e .html,.php,.txt
```

- Setelah perintah diatas jalankan, ditemukan halaman `flag.html`. Selanjutnya kita buka halaman tersebut dibrowser dengan URL `http://ip:port/webfuzzing_hidden_path/flag/flag.html`. Setelah dibuka halaman tersebut berisi flag

- **Answer:**
```sh
HTB{w3b_f1l3_fuzz1ng_fl4g}
```

## Recursive Fuzzing
- Jalankan web target terlebih dahulu
- **Question:** Recursively fuzz the "recursive_fuzz" path on the target system (ie http://IP:PORT/recursive_fuzz/) to find the flag.

- Jalankan tool `ffuf` untuk menemukan direktori web tersembunyi
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://ip:port/recursive_fuzz/FUZZ -c -ic -e .html -recursion -recursion-depth 2 -fc 403
```

- Pada tahap pertama ditemukan path `/level1`

- Pada tahap berikutnya ditemukan path `/level2` sehingga URL yang didapat adalah `http://ip:port/recursive_fuzz/level1/level2`


- Setiap tahap pada proses diatas memerlukan waktu kurang lebih 36 menit sedangkan web hanya berjalan dalam waktu 90 menit sehingga kita kehabisan waktu dan perlu menghidupkan ulang web target. Setelah web target dihidupkan ulang, IP dan port mungkin berbeda dari sebelumnya sehingga anda perlu menggantinya

- Jalankan tool `ffuf` untuk menemukan direktori web tersembunyi `/level1/level2/`
```sh
ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://ip:port/recursive_fuzz/level1/level2/FUZZ -c -ic -e .html -fc 403 -recursion -recursion-depth 2
```

- Pada tahap pertama ditemukan path `/level3`


- Pada tahap berikutnya ditemukan path `/threatcon_level2` sehingga URL yang didapat adalah `http://ip:port/recursive_fuzz/level1/level2/level3/threatcon_level2`

- Setelah dilakukan pengecekan di browser URL diatas berisi flag

- **Answer:**
```sh
HTB{d33p3r_d1rector1es_ar3_c00l}
```