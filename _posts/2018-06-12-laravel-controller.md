---
layout: post
title:  "Laravel 6 - Controller #4"
author: Jefri
categories: [ Laravel, Laravel 6, Tutorial Laravel 6, Laravel 6 Controller]
image: assets/images/logo-laravel.jpg
---

Controller adalah sebuah kelas yang fungsinya untuk menghandle permintaan-permintaan yang dilakukan oleh user dengan data yang akan ditampilkan dari database, dan juga mengatur halaman apa yang akan ditampilkan. 



#### Membuat Controller

Untuk membuat sebuah kelas controller baru, dapat dilakukan menggunakan command `php artisan`. Buka command prompt anda, kemudian ketikan perintah berikut ini, untuk membuat sebuah controller baru dengan nama `UserController`

```php
php artisan make:controller UserController
```

maka secara otomatis muncul file baru di dalam folder `app/Http/Controller` dengan nama `UserController`  yang isinya sebagai berikut : 

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller
{
    //
}

```

Saya akan coba membuat sebuah metode yang nantinya akan mengembalikan halaman `welcome` default Laravel, seperti berikut ini

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class UserController extends Controller
{
    function show() {
    	return view('welcome');
    }
}

```

Kemudian edit file `app/routes/web.php` menjadi berikut : 

```php
Route::get('/', 'UserController@show');
```

ketika kita membuka halaman `http://localhost:8000` maka secara otomatis muncul halaman default awal Laravel.
Jika kita ingin membuat folder di dalam folder `app/Http/Controller` misalkan saja, folder `User`, maka settingan `Routes` akan menjadi seperti berikut ini : 

```php
Route::get('/', 'User\UserController@show');
```


#### Single Action Controller

Jika kita ingin membuat sebuah controller, yang isinya hanya memiliki 1 buah fungsi atau methode saja kita dapat membuat menambahkan `__invoke` di dalam kelas controller tersebut. `Single Action Controller` biasa digunakan untuk mempermudah dalam melakukan maintenance program, atau melakukan perubahan di sebuah controller, misalkan saja controller yang kita buat berisi ribuan line program.

Untuk membuat controller baru, dengan metode `__invoke` otomatis didalamnya, dapat dilakukan dengan cara menambahkan perintah `--invokable` di command php artisan seperti berikut ini : 

```php
php artisan make:controller UserController --invokable
```

Sedangkan untuk settingan `app/routes/web.php` akan menjadi seperti berikut ini : 

```php
Route::get('/', 'UserController');
```


#### Resource Controllers

