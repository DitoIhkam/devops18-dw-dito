# 1. Definisi DevOps

DevOps adalah kepanjangan dari Developer Operations, yang pekerjaan nya menghubungkan antara pengembang software (Developer) dengan IT Operation yang nantinya akan mengoperasikan aplikasi/software hingga sampai ke end-user/consumer. DevOps diperlukan agar bisa mempersingkat waktu mulai dari pengembangan software/aplikasi, hingga nanti nya bisa sampai ke end-user.

# 2. LifeCycle DevOps
 

## 2.1 Continuous Development
Continuous Development merupakan fase planning dan coding pada software/aplikasi. Disini tugas DevOps engineer adalah memahami planning dari tim development sehingga kita dapat membantu mempercepat proses dari development, namun disini kita akan lebih aktif membantu dalam source code management dimana kita membantu memeriksa perubahan dalam setiap  commit yang ada di Repository.

Tools umum yang digunakan : GitHub, BitBucket, Git


## 2.2 Continuous Integration
Continuous Integration merupakan fase dimana kita akan membantu dalam eksekusi proses testing, jika ada penambahan atau pembuatan fitur baru maka Continuous Integration akan menjadi titik dimana kita mengintegrasikan perubahan-perubahan yang di commit oleh tim developer, membantu tracking jika ada masalah pada saat source code diintegrasikan. 


## 2.3 Continuous Testing
Jika tadi Continuous Integration lebih fokus ke dalam integrasi code, Continuous Testing adalah fase dimana kita mulai eksekusi testing untuk mencari segala bentuk bug atau error. Disini kita akan fokus membantu team QA (Quality Assurance) untuk memastikan titik dimana bug/error tersebut agar tim developer dapat dibantu dalam perbaikannya. Docker juga dapat digunakan untuk melakukan test apakah aplikasi berjalan dengan baik atau tidak.

Tools umum yang digunakan: Selenium, JUnit, TestNG dsb. 


## 2.4 Continuous Deployment
Setelah melalui bug fixing, source code management dan automation testing, akhirnya kita sampai di fase deployment, dimana fitur/aplikasi sudah siap dirilis ke publik.

Ini merupakan salah satu lifecycle dimana Continuous Deployment akan membantu mempercepat pekerjaan kita melalui proses otomasi deployment yang reliable dan efisien. Menggunakan tools seperti Ansible, konfigurasi sebuah fitur atau app hanya membutuhkan script dan poof!, berubah sudah konfigurasi aplikasi tersebut.

Tools umum yang digunakan: Ansible, Puppet, Vargant dsb. 


## 2.5 Continuous Monitoring
Dalam setiap deployment, kita pasti butuh data atau metrics untuk mengetahui apa yang bisa dibenahi atau diperbaharui, sehingga Continuous Monitoring merupakan salah satu lifecycle yang crucial, karena agar kita  bisa memaksimalkan aplikasi yang kita deploy, kita juga harus mengetahui seberapa banyak resource yang terpakai, untuk menghindari problem seperti low memory & storage atau untuk memaksimalkan penggunaan resource yang ada. 

Tools umum yang digunakan: Prometheus + Grafana, Nagios, Splunk dsb. 


## 2.6 Continuous Feedback
Deployment Agile akan mendapatkan feedback langsung melalui pengguna aplikasi/fitur mereka, namun berbeda dengan DevOps dimana mereka bisa mencari feedback dari para developer atau client mereka, bisa juga dari hasil monitoring sehingga para DevOps Engineer bisa menganalisa data dan feedback tersebut sehingga aplikasi/fitur dapat dikembangkan lagi


## 2.7 Continuous Operations
Disini, setelah kita menjalankan berbagai lifecycle DevOps, Continuous Operations merupakan step terakhir untuk merawat aplikasi/fitur kedepannya, melalui proses otomatis, deteksi masalah dan pembuatan versi aplikasi/fitur yang lebih baik sehingga dapat mengeliminasi hal-hal yang dapat memperlambat development. Dari step-step yang sudah kita lakukan, ini akan menambah efisiensi development dan memperkuat fitur produk sehingga kita bisa menarik pelanggan lebih banyak lagi.


# 3. Installasi Ubuntu Server menggunakan VMware Workstation

Installasi ubuntu server menggunakan vmware saya buat melalui video, bisa dilihat link dibawah ini :

https://bit.ly/TaskWeek1_IhkamAudito_DumbWays
