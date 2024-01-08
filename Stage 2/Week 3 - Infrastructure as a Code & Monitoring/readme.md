# Terraform Docker

Task :
## 1. Membuat Terraform untuk mendeploy docker image wayshub-fe
## 2. praktekan penggunaan terraform dari pembuatan hingga resource dihancurkan


Sebelum membuat terraform untuk docker, kita perlu menginstall terraform dan docker  terlebih dahulu, disini saya akan menjelaskan khususnya menginstall terraform didalam cloud AppServer.

I. pastikan sistem Anda mutakhir dan Anda telah menginstal paket gnupg, software-properties-common, dan curl yang diinstal

```
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
```

II. Install the HashiCorp GPG key.
```
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg

```

III. Verifikasi key's fingerprint.
```
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
```

IV. Tambahkan repositori resmi HashiCorp ke sistem Anda
```
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```

V. Unduh informasi paket dari HashiCorp.
```
sudo apt update
```

VI. Instal Terraform dari repositori baru.
```
sudo apt-get install terraform
```

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/0.0%20Terraform%20install.png?raw=true)
++++++++++++++++++++++++++++++++++++++
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/0.1%20Terraform%20install.png?raw=true)

source : https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

Setelah menginstall terraform dan dependensinya, saya membuat file terraform dengan nama `docker.tf` yang berekstensi `tf` didalam folder terraform dengan server cloud AppServer.

```
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = ">= 2.0.0"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name = "kelompok2/fe-way"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = "kelompok2/fe-way"
  name  = "frontend"
  ports {
    internal = 3000
    external = 3001
  }
}
```

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/1.%20Terraform%20Docker%20di%20AppServer.png?raw=true)

lalu gunakan perintah2 dibawah ini untuk menjalankan terraform

I. ``` terraform init ``` berfungsi untuk Inisialisasi Konfigurasi terraform
II. ``` terraform validate``` digunakan untuk memvalidasi konfigurasi Terraform
III. ``` terraform plan``` berfungsi untuk melihat rencana2 yang akan dijalankan didalam script terraform yang sudah kita buat
IV. ``` terraform apply``` berguna untuk menerapkan semua yang direncanakan didalam terraform

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/2.%20T%20init.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/2.1%20T%20apply.png?raw=true)

cek image dan container apabila sudah diterapkan terraform nya
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/3.%20Images%20dan%20container.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/4.%20Hasil%20Wayshub.png?raw=true)

V. ```terraform destroy``` berfungsi untuk menghancurkan sumber daya yang sudah kita kelola

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/5.%20T%20Destroy.png?raw=true)


# Ansible

## Task :
### 1. Membuat Terraform untuk mendeploy docker image wayshub-fe
### 2. praktekan penggunaan terraform dari pembuatan hingga resource dihancurkan

**AppServer**
- Membuat user baru, gunakan login ssh key
- Instalasi Docker & node-exporter
- **buat konfigurasi prometheus (Monitoring)**
  - On top docker menjalankan Grafana & Prometheus

**Gateway**
- Membuat user baru, gunakan login ssh key
- Instalasi nginx
- Buat konfigurasi proxy lalu masukkan kedalam gateway
- Gunakan docker-compose untuk deploy aplikasi wayshub-frontend

### Install Ansible

Pastikan python berjalan di ubuntu, ini seharusnya sudah menjadi default dari ubuntu itu sendiri. Gunakan perintah dibawah untuk menginstall ansible  didalam lokal server
```
sudo apt install ansible
```

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/7.%20INstall%20ansible.png?raw=true)


### konfigurasi ansible

Disini saya membuat ansible.cfg yang berfungsi untuk mengkoneksikan ssh dan Inventory yang berfungsi untuk menamakan host IP

`ansible.cfg`
```
[defaults]
inventory = Inventory
private_key_file = ~/.ssh/id_rsa
host_key_checking = false
interpreter_python = auto_silent
```
`Inventory`
```
[appserver]
103.175.221.143

[gateway]
103.175.217.129

[all:vars]
ansible_user="ditoihkam"
```
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/8.%20Konfigurasi%20ansible.png?raw=true)


### Setup AppServer
nantinya juga kita akan mengkonfigurasi prometheus, maka dari itu saya akan membuat prometheus.yml terlebih dahulu yang nantinya akan dicopy paste ke server tujuan

`prometheus.yml`
```
scrape_configs:
  - job_name: Grafana
    scrape_interval: 5s
    static_configs:
      - targets:
        - nodeapp.ditoihkamc.studentdumbways.my.id
        - nodegate.ditoihkamc.studentdumbways.my.id
```

yang terakhir dibagian appserver, kita buat script ansible untuk membuat user, menginstall docker, pull and run node-exporter ke semua server, serta khususnya di bagian appserver kita menginstall dan menjalankan grafana dan prometheus serte mengcopy prometheus.yml ke appserver

`ansible-appserver.yml`
```
- name: Set up user
  hosts: all
  become: true
  tasks:
    - name: Create user
      user:
        name: dito-dw18
        groups: sudo
        state: present
        shell: /bin/bash
        system: no
        createhome: yes
        home: /home/dito-dw18
        password: "$5$qNMJo6MOf3wcBCZ$ZRjvJ9W4ES0IA9rsvXpwe4qtnlrkYs/fOjpmN9Yyb38" #dito625


- hosts: all
  become: true
  vars:
    user: ditoihkam
  tasks:
    - name: Install Docker Dependencies
      apt:
        update_cache: yes
        name:
          - lsb-release
          - ca-certificates
          - curl
          - gnupg

    - name: Install GPG Key for Docker
      apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg

    - name: Add Docker APT Repository
      apt_repository:
        repo: deb https://download.docker.com/linux/ubuntu focal stable

    - name: Install Docker Engine
      apt:
        update_cache: yes
        name:
          - docker-ce
          - docker-ce-cli
          - containerd.io

    - name: Install Docker Compose
      apt:
        name: docker-compose
        state: latest
        update_cache: yes

    - name: Install Python Dependencies
      apt:
        name: python3-pip
        state: latest
        update_cache: yes

    - name: Install Docker SDK for Python
      pip:
        name: docker
        state: latest
        executable: pip3

    - name: Add user to the docker group
      user:
        name: "{{ user }}"
        groups: docker
        append: yes
        state: present

    - name: Start Docker service
      service:
        name: docker
        state: started

    - name: Enable Docker on boot
      service:
        name: docker
        enabled: yes



    - name: Pull the bitnami/node-exporter Docker image
      docker_image:
        name: bitnami/node-exporter
        source: pull

    - name: Run the Node Exporter container
      docker_container:
        name: node-exp
        image: bitnami/node-exporter
        state: started
        restart_policy: unless-stopped
        published_ports:
          - "9100:9100"




- name: Deploy Prometheus and Grafana top on Docker
  hosts: appserver
  become: yes

  tasks:

    - name: Pull Grafana Docker image
      docker_image:
        name: grafana/grafana
        source: pull

    - name: Run Grafana container
      docker_container:
        name: Grafana-container
        image: grafana/grafana
        state: started
        restart_policy: unless-stopped
        published_ports:
          - "3000:3000"

    - name: Pull Prometheus Docker image
      docker_image:
        name: bitnami/prometheus
        source: pull

    - name: Create a directory if it doesn't exist
      ansible.builtin.file:
        path: /home/ditoihkam/prometheus
        state: directory
        mode: '0755'

    - name: Copy prometheus config
      copy:
        src: /home/ditoihkam/ias/prometheus.yml
        dest: /home/ditoihkam/prometheus/prometheus.yml

    - name: Run Prometheus container
      docker_container:
        name: Prometheus-container
        image: bitnami/prometheus
        state: started
        volumes:
          - /home/ditoihkam/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml
        restart_policy: unless-stopped
        published_ports:
          - "9090:9090"
```

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/9.%20install%20ansible-playbook%20appserver.png?raw=true)
>jangan lupa untuk menginstall whois dan menjalankan whois

### Setup Gateway

- Pertama, setup dns cloudflare terlebih dahulu untuk reverse proxy

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/10.%20DNS%20CloudFlare.png?raw=true)

- kemudian saya menyiapkan beberapa file yang nanti akan dicopy ke server tujuan
1. reverse proxy
2. Dockerfile
3. docker-compose.yml
`reverseproxy.conf`
```
server {
    server_name nodeapp.ditoihkamc.studentdumbways.my.id;

    location / {
             proxy_pass http://103.175.221.143:9100;
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
             proxy_set_header X-Forwarded-Proto $scheme;
    }
}



server {
    server_name nodegate.ditoihkamc.studentdumbways.my.id;

    location / {
             proxy_pass http://103.175.217.129:9100;
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
             proxy_set_header X-Forwarded-Proto $scheme;
    }
}



server {
    server_name prom.ditoihkamc.studentdumbways.my.id;

    location / {
             proxy_pass http://103.175.221.143:9090;
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
             proxy_set_header X-Forwarded-Proto $scheme;
    }
}



server {
    server_name graf.ditoihkamc.studentdumbways.my.id;

    location / {
             proxy_pass http://103.175.221.143:3000;
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
             proxy_set_header X-Forwarded-Proto $scheme;
    }
}



server {
    server_name ditoihkamc.studentdumbways.my.id;

    location / {
             proxy_pass http://103.175.217.129:3000;
             proxy_set_header Host $host;
             proxy_set_header X-Real-IP $remote_addr;
             proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
             proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
`Dockerfile`
```
FROM node:14.21.3-alpine
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3000
CMD [ "npm", "start"]
```
`docker-compose.yml`
```
version: "3.7"
services:

  frontend:
    build: ./wayshub-frontend
    container_name: wayshub-fe
    stdin_open: true
    ports:
      - 3000:3000
```

- lalu siapkan script ansible untuk gateway yang nantinya kita akan menginstall nginx, mengcopy file yang dibutuhkan dan mengcloning wayshub fe. gunakan perintah ansible-playbook

`ansible-gateway.yml`
```
---
- become: true
  gather_facts: false
  hosts: gateway
  tasks:
    - name: Installing nginx
      apt:
        name: nginx
        state: latest
        update_cache: yes
    - name: Start nginx
      service:
        name: nginx
        state: started
    - name: Copy reverse-proxy
      copy:
        src: /home/ditoihkam/ias/rproxy.conf
        dest: /etc/nginx/sites-enabled/rproxy.conf
    - name: Reload Nginx
      service:
        name: nginx
        state: reloaded



    - name: Clone GitHub Repository
      git:
        repo: https://github.com/dumbwaysdev/wayshub-frontend
        dest: /home/ditoihkam/wayshub-frontend
      when: not ansible_check_mode


    - name: Copy Dockerfile fe
      copy:
        src: /home/ditoihkam/ias/Dockerfile
        dest: /home/ditoihkam/wayshub-frontend/Dockerfile
      when: not ansible_check_mode


    - name: Copy Docker-compose.yml
      copy:
        src: /home/ditoihkam/ias/docker-compose.yml
        dest: /home/ditoihkam/docker-compose.yml
      when: not ansible_check_mode


    - name: Run docker-compose
      docker_compose:
        project_src: /home/ditoihkam/
        state: present
```

terakhir jangan lupa untuk menginstall certbot ssl

```
---
- become: true
  gather_facts: false
  hosts: gateway
  tasks:

    - name: Install Certbot with Snap
      snap:
        name: certbot
        classic: yes
        state: present
      become: yes


    - name: Obtain and install SSL certificate with Certbot Nginx Node Exporter Gateway
      command: certbot --nginx -d nodegate.ditoihkamc.studentdumbways.my.id --non-interactive --agree-tos --email ditoihkam@gmail.com
      become: yes


    - name: Obtain and install SSL certificate with Certbot Nginx Node Exporter AppServer
      command: certbot --nginx -d nodeapp.ditoihkamc.studentdumbways.my.id --non-interactive --agree-tos --email ditoihkam@gmail.com
      become: yes


    - name: Obtain and install SSL certificate with Certbot Nginx prometheus
      command: certbot --nginx -d prom.ditoihkamc.studentdumbways.my.id --non-interactive --agree-tos --email ditoihkam@gmail.com
      become: yes


    - name: Obtain and install SSL certificate with Certbot Nginx Grafana
      command: certbot --nginx -d graf.ditoihkamc.studentdumbways.my.id --non-interactive --agree-tos --email ditoihkam@gmail.com
      become: yes
```

## Monitoring

###  Node-exporter
- Pastikan node-exporter berjalan dimasing masing server

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/12.1%20node-exp%20monitoring.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/12.2%20node-exp%20monitoring.png?raw=true)


### Prometheus
- Pastikan prometheus berhasil menargetkan ke setiap node-exporter
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/13.%20Prometehus.png?raw=true)


### Grafana
- Masuk ke grafana dengan user dan password ```admin```, lalu dibagian beranda, add data source terlebih dahulu, lalu konfigurasikan add data source

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/14.1%20login%20grafana.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/14.2%20Beranda%20grafana.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/14.3%20add%20data%20source.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/14.4%20konfigurasi%20data%20source.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/14.5%20konfigurasi%20data%20source.png?raw=true)

- Lalu sekarang kita akan membuat dashboard grafana menggunakan dashboard import 1860

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/15.1%20Setting%20dashboard%20grafana.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/15.2%20Setting%20dashboard%20grafana.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/15.3%20Setting%20dashboard%20grafana.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/15.4%20Setting%20dashboard%20grafana.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/15.5%20hasil.png?raw=true)

### Alerting

![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/16.1%20Alert%20rule.png?raw=true)
![alt text](https://github.com/DitoIhkam/devops17-dumbways-ihkam-audito/blob/main/Stage%202/Gambar%20Week%203/16.2%20Alert%20rule.png?raw=true)
![alt text](?raw=true)
