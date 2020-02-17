---
layout: post
title:  "Laravel 6 - Middleware"
author: Jefri
categories: [ Laravel, Laravel 6, Tutorial Laravel 6, Laravel 6 Middleware ]
image: assets/images/logo-laravel.jpg
---

Laravel Middleware adalah sebuah mekanisme yang digunakan untuk melakukan validasi dan filter dari setiap `request` http yang dikirimkan oleh user. Contoh Middleware yang paling sering dibuat adalah Middleware untuk melakukan pengecekan apakah user telah login atau hak akses user.

#### Membuat Middleware

Untuk membuat sebuah middleware, gunakan `command artisan` seperti berikut ini : 

```js
php artisan make:middleware CheckAge
```

Command diatas, akan membuat sebuah file baru di dalam folder `app/Http/Middleware` dengan nama `CheckAge`. 
`middleware` ini digunakan untuk membatasi parameter `Age` yang dikirimkan melalui routes, sebelum mengakses `request`. Jika nilai yang dikirimkan kurang dari 200, maka akan diredirect ke halaman welcome.

```php
<?php

namespace App\Http\Middleware;

use Closure;

class CheckAge
{
    /**
     * Handle an incoming request.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  \Closure  $next
     * @return mixed
     */
    public function handle($request, Closure $next)
    {
        if ($request->age <= 200) {
            return redirect('/');
        }

        return $next($request);
    }
}
```


#### Mendaftarkan Middleware

Setelah selesai membuat `middleware` diatas, langkah selanjutnya yang perlu dilakukan adalah mendaftarkan middleware yang dibuat ke dalam file konfigurasi `app/Http/Kernel`. Beberapa hal yang perlu kita ketahui mengenai middleware : 


##### 1. Middleware Untuk Routes

Untuk membuat middleware yang digunakan untuk menghandle `request` http di routes, dengan menuliskan nama middleware dan `path` middleware di dalam variable array `$routeMiddleware` seperti berikut ini : 

```php
	protected $routeMiddleware = [
	    'checkAge' => \App\Http\Middleware\CheckAge::class,
	    'auth.basic' => \Illuminate\Auth\Middleware\AuthenticateWithBasicAuth::class,
	    'bindings' => \Illuminate\Routing\Middleware\SubstituteBindings::class,
	    'cache.headers' => \Illuminate\Http\Middleware\SetCacheHeaders::class,
	    'can' => \Illuminate\Auth\Middleware\Authorize::class,
	    'guest' => \App\Http\Middleware\RedirectIfAuthenticated::class,
	    'password.confirm' => \Illuminate\Auth\Middleware\RequirePassword::class,
	    'signed' => \Illuminate\Routing\Middleware\ValidateSignature::class,
	    'throttle' => \Illuminate\Routing\Middleware\ThrottleRequests::class,
	    'verified' => \Illuminate\Auth\Middleware\EnsureEmailIsVerified::class,
	];
```

Setelah itu edit file `routes/web.api` menjadi seperti berikut ini : 

```php
Route::get('/', function () {
    return view('welcome');
});

Route::get('/page/{age}', function($age) {
	return 'Usia Anda : '.$age;
})->middleware('checkAge');

```

Kemudian setelah itu buka browser, dan ketikan pada halaman browser `http://localhost:8000/page/225` maka akan muncul tampilan `Usia Anda 225` jika kita memanggil url `http://localhost:8000/page/50` maka secara otomatis, akan muncul halaman awal, karena kondisi usia yang dibawah 200.


##### 2. Group Middleware

Jika kita memiliki banyak middleware, dan ingin mengelompokanya untuk proses tertentu, kita dapat melakukan dengan mendaftarkan middleware-middleware yang kita buat dalam variabel `middlewareGroups` di dalam file `app/Http/Kernel.php`, sehingga ketika di dalam `routes` kita tidak perlu mendefinisikan 1 persatu route yang kita buat.

Secara default Laravel membuat 2 group middleware yatiu `web` dan `api` yang fungsinya untuk halaman Web UI dan API.

```php
/**
 * The application's route middleware groups.
 *
 * @var array
 */
protected $middlewareGroups = [
    'web' => [
        \App\Http\Middleware\EncryptCookies::class,
        \Illuminate\Cookie\Middleware\AddQueuedCookiesToResponse::class,
        \Illuminate\Session\Middleware\StartSession::class,
        // \Illuminate\Session\Middleware\AuthenticateSession::class,
        \Illuminate\View\Middleware\ShareErrorsFromSession::class,
        \App\Http\Middleware\VerifyCsrfToken::class,
        \Illuminate\Routing\Middleware\SubstituteBindings::class,
    ],

    'api' => [
        'throttle:60,1',
        \Illuminate\Routing\Middleware\SubstituteBindings::class,
    ],
];
```

Setelah mendaftarkan route-route yang dibuat dalam `middlewareGroups`, berikut contoh bagaimana menggunakan middleware group yang sudah di daftarkan diatas : 

```php
Route::get('/', function () {
    //
})->middleware('web');
```


##### 3. Pengurutan Middleware

Kita dapat melakukan konfigurasi, urutan middleware dijalankan. Caranya adalah mendaftarkan middleware yang kita buat didalam `app/Http/Kernel.php`  didalam variable `middlewarePriority`. 

```php


/**
 * The priority-sorted list of middleware.
 *
 * This forces non-global middleware to always be in the given order.
 *
 * @var array
 */
protected $middlewarePriority = [
    \Illuminate\Session\Middleware\StartSession::class,
    \Illuminate\View\Middleware\ShareErrorsFromSession::class,
    \App\Http\Middleware\Authenticate::class,
    \Illuminate\Session\Middleware\AuthenticateSession::class,
    \Illuminate\Routing\Middleware\SubstituteBindings::class,
    \Illuminate\Auth\Middleware\Authorize::class,
];
```

Demikianlah tutorial mengenai `Laravel Middleware` ini, semoga tulisan saya ini mudah dipahami. Mohon maaf jika ada kekurangan.