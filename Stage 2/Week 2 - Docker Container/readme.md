[Teks Tautan](URL)

# Kelompok 3

Anggota :
* Wilson
* Ihkam Audito
* Jerry

# Docker


Docker adalah platform perangkat lunak terbuka yang memungkinkan Anda untuk membangun, menguji, dan menyebarkan aplikasi dengan cepat. Docker menggunakan containerisasi untuk membuat dan mengelola aplikasi. 

Disini saya akan mencoba untuk mendeploy website wayshub yaitu website streaming video menggunakan docker, mengemasnya menjadi lebih fleksibel.

# Setup VM

## Requirements
Buat 3 VM dengan spesifikasi sebagai berikut

| VM | CPU | RAM | Storage |
| -- | -- | -- | -- |
| Appserver | 2 Core | 2 GB | 60 GB |
| Gateway | 1 Core | 1 GB | 60 GB |
| CI/CD | 2 Core | 2 GB | 60 GB |

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar/1.%20VM%201.png?raw=true)
-
-
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar/2.%20VM%202.png?raw=true)

# Setup Docker

Pertama, kita install  gpg key dan menambahkan repository ke apt sources, sesuai yang ada di instruksi website docker installasi menggunakan [Ubuntu engine](https://docs.docker.com/engine/install/ubuntu/)

```
 # Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

```
# Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```
#install docker
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

> apabila menggunakan idch, pastikan mirror diganti dengan archive ubuntu
>sudo nano /etc/apt/sources.list
http://archive.ubuntu.com/ubuntu

(gambar )

berikutnya melakukan setup root commmander untuk memberikan akses user untuk menjalankan perintah tanpa menggunakan sudo

```
sudo usermod -aG docker (user)
sudo su (user)
docker version
```

(gambar docker version)

# Deploy aplkasi on top docker

## Frontend Wayshub

clone frontend wayshub terlebih dahulu
```
git clone https://github.com/dumbwaysdev/wayshub-frontend
```
(gambar clone)

lakukan integrasi frontend 	dengan backend serta buat DOckerfile

```
nano api.js
nano Dockerfile
```
(gambar nano keduanya)
(gambar setting api https)

```
FROM node:14.21.3-alpine
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD [ "npm", "start"]
```

## Backend Wayshub

Clone Backend terlebih dahulu

```
git clone https://github.com/dumbwaysdev/wayshub-backend
```
Lalu integrasikan backend ke database serta membuat dockerfile

```
nano config/config.json
nano Dockerfile
```

(gambar nano)
(gambar config.json)

```
FROM node:14.21.3-alpine
WORKDIR /app

COPY . .
RUN npm install

RUN npm install sequelize-cli -g

ENV DB_HOST=db-wayshub
ENV DB_USERNAME=kel3-appserver
ENV DB_PASSWORD=katasand1

RUN sequelize db:create

COPY migrations /migrations
RUN sequelize db:migrate

EXPOSE 5000
CMD [ "npm", "start"]
```

## Docker compose

Buat file serta edit isi nya sebagai berikut dengan nama `docker-compose.yml`

```
version: "3.8"
services:
  db:
    image: mysql
    container_name: db-wayshub
    ports:
      - 3306:3306
    volumes:
      - ~/mysqldata:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=katasand1
      - MYSQL_USER=kel3-appserver
      - MYSQL_PASSWORD=katasand1
      - MYSQL_DATABASE=db-wayshub

  backend:
    depends_on:
      - db
    build: ./wayshub-backend
    container_name: wayshub-be
    stdin_open: true
    ports:
      - 5000:5000

  frontend:
    build: ./wayshub-frontend
    container_name: wayshub-fe
    stdin_open: true
    ports:
      - 3000:3000
```

lalu lakukan perintah berikut untuk menjalankannya

```
docker compose up -d
```

(gambar ketika docker compose)

## Docker push images

Login terlebih dahulu menggunakan username dan password masing2

```
docker login
```

(gambar docker login)

Kemudian berikan tag dan push pada image

```
docker tag ditoihkam-frontend kelompok2/wayshub-frontend
```

```
docker push kelompok2/wayshub-frontend
```

(gambar push nya)

## Konfigurasi Reverse Proxy

Sekarang saya akan mengkonfigurasikannya di server gateway, pertama saya akan menginstall NGINX terlebih dahulu

```
sudo apt update
sudo apt install nginx
```
(gambar installasi nginx)

Setelah selesai install nginx, buat reverse proxy dan install ssl di bagian /etc/nginx/sites-enabled

```
cd /etc/nginx/sites-enabled
```
buat file didalam ini dengan perintah sudo dan nama yang diinginkan
```
sudo nano rporxy.conf
```
lalu edit reverse proxy seperti dibawah

```
server { 
    server_name nama.studentdumbways.my.id; 
    
    location / { 
             proxy_pass http://IPAppServer:3000;
    }
}


server { 
    server_name api.nama.studentdumbways.my.id; 
    
    location / { 
             proxy_pass http://IPAppServer:5000;
    }
}
```

lalu install ssl certbot sesuai panduan web disini  [Certbot SSL](https://certbot.eff.org/instructions?ws=nginx&os=ubuntufocal)

```
#install certbot
sudo snap install --classic certbot
```
```
#run certbot ssl
sudo certbot --nginx
```

(gambar installasi ssl)

Terakhir reload nginx dengan perintah dibawah agar merefresh nginx
```
sudo systemctl reload nginx
```

hasil mengakses web seperti yang bisa dilihat dibawah ini

(gambar wayshub daftar)
(gambar wayshub login )
