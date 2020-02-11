---
layout: post
title:  "Laravel 6 - Routing #2"
author: Jefri
categories: [ Laravel, Laravel 6, Tutorial Laravel 6, Routing Laravel 6 ]
image: assets/images/logo-laravel.jpg
featured: true
hidden: true
---

Setelah sebelumnya membahas mengenai [Pengenalan dan Installasi Laravel 6]({% post_url 2020-02-10-pengenalan-laravel %}){:target="_blank"}. Saya akan membahas part berikutnya yaitu **Routing**

Fungsi dari routing sendiri untuk mengatur rute lalu lintas dari request-request yang dilakukan oleh user. Berikut dibawah ini adalah contoh dasar, bagaimana menuliskan route dalam laravel : 

```js
Route::get('foo', function () {
    return 'Hello World';
});
```
#### Default Route Files
Saat melakukan installasi Laravel Framework, Secara otomatis Laravel akan membuat 4 Buah file route yaitu : 
1. **Api.php**<br>
	Route ini digunakan untuk mendefinisikan rute-rute yang digunakan untuk API

2. **Channels.php**<br>
	Route ini digunakan untuk mendefinisikan rute semua `event broadcasting channels` di aplikasi yang dibuat

3. **Consele.php**<br>
	Route ini digunakan untuk mendefinisikan rute untuk `consule command` pada saat kita menggunakan artisan.

4. **Web.php**<br>
	Route ini digunakan untuk mendefinisikan rute untuk aplikasi yang kita buat, yang bisa diakses oleh user melalui browser.

Buka file dalam folder `routes/web.php` kemudian ketikan perintah dibawah ini : 

```js
Route::get('hello', function () {
    return 'Hello World';
});
```

sehingga isi dari file routes/web.php menjadi 

```js
Route::get('/', function () {
    return view('welcome');
});

Route::get('hello', function () {
    return 'Hello World';
});
```

Kemudian ketikan url pada browser `http://localhost:8000/hello` maka akan muncul tampilan sebagai berikut :

![contoh-route-1]({{ site.base_url }}/assets/images/tutorial/example-1.png)

Untuk menghubungkan routes yang kita buat dengan controller yang kita miliki dapat dituliskan sebagai berikut : 

```js
Route::get('/user', 'UserController@index');
```

**UserController** Merupakan nama controller yang kita miliki, dan **index** adalah nama method yang akan diakses.

Jika diatas kita telah belajar bagaimana membuat routes dengan metode `GET`, routes juga memiliki beberapa metode lainya, yang dapat digunakan sesuai dengan kebutuhan yang diinginkan.

#### Beberapa Metode Routes 

```js
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
```

Jika kita ingin membuat **Routes** yang dapat diakses oleh metode apa pun kita dapat menggunakan Routes seperti dibawah ini : 

```js
Route::any('/', function () {
    //
});
```

#### Routes Redirect 

Kita dapat membuat routes, yang dapat mengalihkan url yang akan diakses ke url lain, fungsi ini dapat digunakan, 
ketika parameter yang dikirimkan tidak sesuai atau halaman yang diakses tidak ditemukan. 

Berikut dibawah ini, saya akan membuat contoh routes, ketika kita akan mengakses halaman page 1 otomatis akan dialihkan ke halaman page 2. Tuliskan perintah dibawah ini pada file routes/web.php. setelah itu panggil halaman page1 melalui browser seperti berikut `http://localhost:8000/page1`

```js
Route::redirect('/page1', '/page2');

Route::get('/page2', function(){
	return 'You are in page 2';
})
```
