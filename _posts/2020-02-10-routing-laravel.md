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
	Route ini digunakan untuk mendefinisikan rute untuk `console command` pada saat kita menggunakan artisan.

4. **Web.php**<br>
	Route ini digunakan untuk mendefinisikan rute untuk aplikasi yang kita buat, yang bisa diakses oleh user melalui browser.

Buka file dalam folder `routes/web.php` kemudian ketikan perintah dibawah ini : 

```js
Route::get('hello', function () {
    return 'Hello World';
});
```

sehingga isi dari file `routes/web.php` menjadi 

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

Berikut dibawah ini, saya akan membuat contoh routes, ketika kita akan mengakses halaman page 1 otomatis akan dialihkan ke halaman page 2. Tuliskan perintah dibawah ini pada file `routes/web.php`. setelah itu panggil halaman page1 melalui browser seperti berikut `http://localhost:8000/page1` Maka yang akan tampil url `page2`. 

```js
Route::redirect('/page1', '/page2');

Route::get('/page2', function(){
	return 'You are in page 2';
})
``` 

#### Routes View

Berbeda dengan routes-routes diatas, Routes view digunakan untuk menampilkan halaman view secara langsung melalui route. Berikut dibawah ini contoh bagaimana menggunakan Routes View, edit file `routes/web.php` 
edit kode default route dibawah ini : 

```js
Route::get('/', function () {
    return view('welcome');
});
```

menjadi berikut ini : 

```js
Route::view('/', 'welcome');
```

Maka akan muncul halaman tampilan awal laravel yang sama. Saat menampilkan halaman view menggunakan routes, kita juga bisa menambahkan data parameter. Sebagai contoh berikut ini : 

```js
Route::view('/', 'welcome', ['name'=>'Budi']);
```

Kemudian edit file di dalam folder `resources/views/welcome.blade.php` pada bagian ini, untuk menampilkan variabel yang telah kita kirimkan melalui routes

![contoh-route-1]({{ site.base_url }}/assets/images/tutorial/laravel-route-welcome.png)

#### Routes Parameter

Pada saat membuat routes, kita dapat juga mengirimkan parameter di routes yang akan kita kirimkan, dan melakukan validasi parameter yang akan diterima. Berikut dibawah ini contoh bagaimana membuat routes, dengan variable `name`. 

```js
Route::get('hello/{name?}', function ($name = '') {
    return 'Hello '.$name;
});
```

Setelah menuliskan perintah diatas, kita akan coba memanggil routes yang kita buat dengan cara berikut ini : `http://localhost:8000/hello/Budi` maka akan muncul pada browser text `Hello Budi`. 

Kita dapat melakukan validasi dari variabel yang dikirimkan, seperti contoh, variabel name harus dalam bentuk `string` atau huruf dan variabel `id` harus dalam bentuk numeric dengan contoh seperti berikut ini : 

```js
Route::get('hello/{id}/{name}', function ($id, $name) {
    return 'Hello '.$name.' '.$id;
})->where(['id' => '[0-9]+', 'name' => '[a-z]+']);
```

Sehingga hasil yang muncul akan seperti dibawah ini. Jika kita menginputkan id dengan huruf, maka akan muncul tampilan `404 Not Found`

![contoh-route-1]({{ site.base_url }}/assets/images/tutorial/example-2.png)

#### Routes Names

Kita dapat memberikan nama atau alias untuk route yang kita buat, agar lebih mudah ketika kita ingin memanggil route tersebut. Sebagai contoh saya akan memberikan nama untuk route dibawah ini : 

```js
Route::get('hello/{id}/{name}', function ($id, $name) {
    return 'Hello '.$name.' '.$id;
})->where(['id' => '[0-9]+', 'name' => '[a-z]+'])->name('salam');

Route::get('page1/{id}/{name}', function($id, $name) {
    return redirect()->route('salam', ['id'=>$id, 'name'=>$name]);
})->where(['id' => '[0-9]+', 'name' => '[a-z]+']);
```

ketika saya akan mengakses halaman `http://localhost:8000/page1/1/budi` maka akan secara otomatis akan menampilkan 
halaman `hello` dengan parameter `id` dan `name` yang dikirimkan.

#### Routes Group






