# 1. Penjelasan Distributed Version Control (DVC) 
Distributed Version Control atau disingkat DVC adalah sistem kontrol versi yang memungkinkan pengembang untuk mengelola dan mengontrol perubahan pada kode sumber proyek secara terdistribusi. DVC tidak sama dengan sistem kontrol versi sentralis (CVCS), di mana setiap anggota tim harus terhubung secara langsung ke repositori pusat untuk mengakses kode sumber dan melakukan perubahan.
Contoh nya yaitu Git yang bisa melakukan perubahan dengan push and pull.

# 2. Membuat repository sample yang berisi 3 file dengan isi yang berbeda
1. Buat direktori atau file dengan perintah mkdir (namafile). Dalam hal ini saya membuat direktori menggunakan perintah `mkdir repotask`. Lalu pindah ke direktori tersebut menggunakan perintah cd repotask.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/1.%20Version%20Control%20System/gambar/2.png?raw=true)

2. Buatlah 3 file dengan nama yang diinginkan. Dalam hal ini saya menggunakan perintah `touch file1 file2 file3`. Ketik perintah `git init` di terminal untuk membuat repositori baru. 
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/1.%20Version%20Control%20System/gambar/4.png?raw=true)

3. Tambahkan file ke dalam staging area yang akan disiapkan lebih lanjut untuk di commit. gunakan perintah `git add .`. Ini akan memilih semua file. 
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/1.%20Version%20Control%20System/gambar/5.png?raw=true)

4. Setelah dicek git status file2 siap di commit menggunakan perintah `git status`, ketik perintah `git commit -m "commit 3 files"`. Ini akan mengcommit semua file yang ada di staging area dan menambahkan deskripsi commit 3 files.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/1.%20Version%20Control%20System/gambar/6.png?raw=true)

5. Buat tujuan repository github nya mau diupload ke mana, masukan link ssh yang tersedia di repository github. Ketikan seperti ini `git remote add origin git@github.com:DitoIhkam/devopsdito.git`. Lalu setelah itu kirimkan perubahan yang telah tercommit dari repositori lokal ke repositori yang kita remote di github. ketikk `git push origin master`.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/1.%20Version%20Control%20System/gambar/7.png?raw=true)

6. Terakhir kita bisa lihat bahwa file yang kita buat di repository git kita telah diperbarui ke repository yang kita remote di github seperti gambar dibawah.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/1.%20Version%20Control%20System/gambar/8.png?raw=true)


# 3. Membuat Branch Staging dan Production
1. Kita pastikan bahwa branch hanya 1 yaitu master. Ketik `git branch -a`. Lalu kita buat branchnya dengan mengetikkan `git branch staging` dan `git branch production`.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/1.%20Version%20Control%20System/gambar/11.png?raw=true)

2. Kita commit semua perubahan dengan mengetik perintah `git commit .`
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/1.%20Version%20Control%20System/gambar/13.png?raw=true)

3. Kita push kedua branch itu dengan mengetikan `git push origin staging` dan `git push origin production`
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/1.%20Version%20Control%20System/gambar/14.png?raw=true)

4. Seperti yang bisa kita lihat di repository github, 2 branch sudah ditambahkan seperti yang ada di gambar.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/1.%20Version%20Control%20System/gambar/16.png?raw=true)


# 4. Tiga Command Git yang belum dijelaskan
git tag: Menandai titik tertentu dalam sejarah commit dengan tag.

git reset: Mengatur ulang HEAD dan mencabut perubahan dari staging area atau commit tertentu.

git revert: Membuat commit baru yang membatalkan perubahan yang ada pada commit sebelumnya.
