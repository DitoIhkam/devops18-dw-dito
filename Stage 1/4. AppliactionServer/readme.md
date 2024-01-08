# 1. Perbedaan Monolith dan Microservice

## A. Monolith
* Biasanya, arsitektur monolitik memiliki satu basis data tunggal yang digunakan oleh semua komponen aplikasi.
* Pemeliharaan, pengujian, dan penyebaran perubahan pada aplikasi monolitik dapat menjadi lebih kompleks karena setiap perubahan harus mempengaruhi dan diuji secara menyeluruh pada aplikasi keseluruhan.
* Skalabilitas aplikasi monolitik terbatas karena setiap komponen harus diperlakukan sebagai satu kesatuan dan dapat mengakibatkan overhead yang signifikan saat jumlah pengguna dan beban meningkat.

## B. Microservice
* Skalabilitas aplikasi microservice lebih fleksibel karena masing-masing layanan dapat ditingkatkan secara independen sesuai kebutuhan.
* Pemeliharaan, pengujian, dan penyebaran perubahan pada aplikasi microservice dapat lebih mudah dan cepat karena perubahan hanya mempengaruhi layanan yang terkait.
* Namun, pengelolaan dan pemantauan lingkungan distribusi dapat menjadi lebih kompleks dalam arsitektur microservice.


# 2. Deploy Aplikasi wayshub-frontend (NodeJS)

Dalam mendeploy aplikasi wayshub-frontend, disini saya akan mengacu pada website https://github.com/dumbwaysdev/wayshub-frontend. Berikut untuk langkah-langkah nya 

1. Buat folder direktori dengan menggunakan perintah mkdir (nama folder). Dalam contoh disini saya menggunakan perintah mkdir wayshub, untuk membuat folder yang bernama wayshub.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/1.png?raw=true)

2. Pindah ke dalam file direktori yang sudah kita buat dengan perintah cd (nama folder). Dalam hal ini saya menggunakan perintah cd wayshub.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/2.png?raw=true)

3. Duplikat repositori wayshub-frontend di github kedalam server kita dengan menggunakan perintah git clone (nama website). Dalam hal ini saya mengganakan perintah git clone https://github.com/dumbwaysdev/wayshub-frontend
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/3.png?raw=true)

5. Kita perlu mengintall npm didalam folder ini, untuk memunculkan node modules yang kita perlukan untuk menjalankan wesbite node.js. caranya ketik perintah npm install. Berikut untuk prosesnya.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/4.png?raw=true)

6. Yang terakhir, kita jalankan repositorinya dengan cara ketik npm start. Setelah dijalankan, buka browser dan ketikan ip ubuntu server ke dalam browser. Maka akan muncul website wayshub-frontend yang sudah kita duplikat tadi.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/Screenshot%20(186).png?raw=true)


# 3. Deploy Golang dengan nama sendiri

1. Buat folder direktori dengan menggunakan perintah mkdir (nama folder). Dalam contoh disini saya menggunakan perintah mkdir golang, untuk membuat folder yang bernama golang.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/GO1.png?raw=true)

2. Kita pindah ke direktori yang sudah kita buat menggunakan perintah cd golang, lalu kita install golang dengan perintah berikut `wget https://golang.org/dl/go1.16.5.linux-amd64.tar.gz && sudo su`
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/GO3.png?raw=true)

3. Kita perlu menghapus instalasi golang lama dan mengekstrak instalasi baru di lokasi -C /usr/local, kita jalankan perintah `rm -rf /usr/local/go && tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz && exit`
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/GO4.png?raw=true)

4. Ubah direktori ke bagian awal, lalu kita edit file .bashrc dengan perintah `sudo nano .bashrc`.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/GO5.png?raw=true)

5. Lalu kita perlu menambahkan kalimat `export PATH=$PATH:/usr/local/go/bin` ke paling bawah file ini, agar perintah2 go bisa dijalankan langsung di shell.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/GO6.png?raw=true)

6. Lalu buat file dan edit dengan menjalankan `nano index.go`, isi kode tersebut dengan seperti di gambar. Simpan dan jalankan programnya dengan perintah `go run (nama file)`. Dalam contoh ini saya menggunakan `go run index.go`
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/GO8.png?raw=true)

7. Maka akan tampil hasil seperti dibawah ini nama saya.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/las.png?raw=true)


# 4. Deploy Python Flask nama sendiri

1. Buat folder dengan perintah `mkdir pyproject`. Disini saya membuat folder dengan nama pyproject.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/PY1.png?raw=true)

2. Pindah ke direktori yang telah kita buat dengan perintah `cd pyproject` dan cek python apakah sudah ada atau belum dengan mengetik `python3 -V`
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/PY2.png?raw=true)

3. Kita perlu menginstall PIP atau python install packages untuk bisa menginstall flask. Ketik perintah `sudo apt install python3-pip`. Setelah selesai kita bisa menginstall flask dengan perintah `sudo pip3 install flask`.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/PY3.png?raw=true)

4. Ketiikan `nano index.py` untuk membuat serta mengedit file bernama index.py. edit seperti gambar dibawah ini.
https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/PY44.png

5. Terakhir, jalankan filenya dengan perintah `python3 index.py`
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%201/4.%20Application%20Server/PY5.png?raw=true)
