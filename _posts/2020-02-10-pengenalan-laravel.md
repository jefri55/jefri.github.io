---
layout: post
title:  "Pengenalan dan Installasi Laravel 6"
author: Jefri
categories: [ Laravel, Laravel 6, Tutorial Laravel 6, Installasi Laravel 6 ]
image: assets/images/12.jpg
featured: true
hidden: true
---

Laravel adalah sebuah PHP Framework yang saat ini sedang banyak digunakan, dengan situs resminya di [Laravel Website](https://laravel.com/){:target="_blank"}
Berdasarkan Google Trends di Bulan Jan - Feb Tahun 2020, Laravel lebih popular daripada beberapa PHP Framework lainya. 

![google-trends-laravel]({{ site.baseurl }}/assets/images/google-trend-laravel.png)

Tanpa berbasa-basi pada tahap pengenalan awal ini, saya akan mencoba menjelaskan bagaimana proses installasi dari Laravel. Sebelumnya kita harus menginstall **Web Server** dan **Composer** sebelum melakukan installasi Laravel.
Kemudian, hal yang perlu dipersiapkan berikutnya adalah mempersiapkan Server Requirements dari Laravel, sebelum melakukan installasi :

1. **PHP >= 7.2.0**
2. **BCMath PHP Extension**
3. **Ctype PHP Extension**
4. **JSON PHP Extension**
5. **Mbstring PHP Extension**
6. **OpenSSL PHP Extension**
7. **PDO PHP Extension**
8. **Tokenizer PHP Extension**
9. **XML PHP Extension** 

Setelah Proses diatas telah kita siapakan, proses berikutnya adalah menjalankan perintah berikut melalui command prompt : 

```
composer create-project --prefer-dist laravel/laravel blog
```

![process-install-laravel]({{ site.baseurl }}/assets/images/installasi-laravel.png)

Setelah proses installasi selesai, masuk ke dalam folder `blog` yang kita sudah buat sebelumnya 
```
	cd /var/www/html/blog/
```

Hal yang perlu kita lakukan selanjutnya adalah memberikan permission untuk folder storage, dengan cara seperti berikut ini : 

![process-install-laravel]({{ site.baseurl }}/assets/images/permission-laravel.png)

setelah set permission folder, kemudian ketikan perintah berikut ini, untuk menampilkan halaman laravel 
```
php artisan serve
```

![process-install-laravel]({{ site.baseurl }}/assets/images/halaman-awal-laravel.png)

#### Informasi Direktori

1. **App**
	Direktori inti dari aplikasi yang ingin kita buat, seperti controller, model maupun middleware

2. **Bootstrap**
	Direktori ini berisi cache dari aplikasi yang kita buat

3. **Config**
	Direktori ini berisi semua config-config yang digunakan pada aplikasi yang kita gunakan, seperti database, 
	log, cache dll

4. **Database**
	Direktori ini berisi, migrations, seeds, factories. yang digunakan untuk membuat struktur table yang akan digunakan di aplikasi kita

5. **Public**
	Direktori ini adalah folder yang dapat diakses oleh user, kita melakukan request ke halaman website yang dibuat. Di dalam folder ini juga biasa digunakan untuk menyimpan assets file seperti gambar, css, js, dll.

6. **Resources**
	Direktori ini berisi halaman-halaman website yang akan dibuat, juga berisi file mentah seperti `less, sass, js` sebelum di compile menjadi file `css dan js`

7. **Routes**
	Direktori ini berisi file rute untuk mengatur lalu lintas url yang dapat diakses oleh user.

8. **Storages**
	Direktori ini berisi hasil kompilasi dari file `blade` yang kita buat dalam membuat website.

9. **Tests**
	Direktori ini digunakan untuk melakukan testing, dari project yang kita buat.

10. **Vendor**
	Direktori ini berisi library-library yang kita install melalui composer.


Demikian tutorial singkat, bagaimana melakukan installasi `Laravevl` dan Pengenalan tentang folder-folder yang ada di dalamnya. Mohon Maaf, jika bahasa yang digunakan kurang dapat dimengerti. GBU



