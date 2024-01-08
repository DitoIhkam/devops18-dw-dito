# 1. Instalasi nginx melalui apt

1. Update terlebih dahulu dengan `sudo apt update`. Lalu langsung install nginx dengan perintah `sudo apt install nginx`.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/3.%20Web%20Server%20and%20Load%20Balancing/image/NGINX1.png?raw=true)

2. Lalu kita cek status nya apakah sudah aktif nginx nya dengan perintah `sudo systemctl status nginx`
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/3.%20Web%20Server%20and%20Load%20Balancing/image/NGINX2.png?raw=true)

3. Terakhir kita jalankan di browser dengan ip server kita apabila nginx sudah aktif. Tampilan akan seperti ini.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/3.%20Web%20Server%20and%20Load%20Balancing/image/NGINX3.png?raw=true)


# 2. Menjalankan aplikasi dumbflix menggunakan PM2

1. Buat direktori, disini saya menggunakan perintah `mkdir pm2`. Jangan lupa untuk berpindah ke direktori tersebut dengan perintah cd pm2.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/3.%20Web%20Server%20and%20Load%20Balancing/ImagePM2/PM2%201.png?raw=true)

2. Buat kloningan dumbflix dengan menggunakan perintah `git clone https://github.com/dumbwaysdev/dumbflix-frontend.git`. Lalu kita install pm2 dengan cara mengetik perintah `sudo npm install -g pm2
`. ![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/3.%20Web%20Server%20and%20Load%20Balancing/ImagePM2/PM2%202.png?raw=true)

3. Kita pindah ke direktori dumbflix front end dengan perintah `cd dumbflix-frontend`. Lalu kita install npm dengan perintah `npm install`.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/3.%20Web%20Server%20and%20Load%20Balancing/ImagePM2/PM2%203.png?raw=true)

4. Kita mulai PM2 untuk menjalankan web frontend dengan perintah `pm2 start npm --name "dumbflix" -- start`.
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/3.%20Web%20Server%20and%20Load%20Balancing/ImagePM2/PM2%204.png?raw=true)

5. Kita masukkan ip server kita ke web server dengan port 3000. Hasilnya akan seperti di gambar...
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/WEEK%202/3.%20Web%20Server%20and%20Load%20Balancing/ImagePM2/PM2%205.png?raw=true)
