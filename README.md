# Crypt  for laravel5.*  or  lumen

---
[![](https://travis-ci.org/ShaoZeMing/laravel-crypt.svg?branch=master)](https://travis-ci.org/ShaoZeMing/laravel-crypt) 
[![](https://img.shields.io/packagist/v/ShaoZeMing/laravel-crypt.svg)](https://packagist.org/packages/shaozeming/laravel-crypt) 
[![](https://img.shields.io/packagist/dt/ShaoZeMing/laravel-crypt.svg)](https://packagist.org/packages/shaozeming/laravel-crypt)

## Installing

```shell
$ composer require shaozeming/laravel-crypt -v
```
### Laravel



```php
// config/app.php

    'providers' => [
        //...
        ShaoZeMing\LaravelCrypt\CryptServiceProvider::class,    //This is default in laravel 5.5
    ],
```

And publish the config file: 

```shell
$ php artisan vendor:publish --provider=ShaoZeMing\\LaravelCrypt\\CryptServiceProvider
```

if you want to use facade mode, you can register a facade name what you want to use, for example `crypt`: 

```php
// config/app.php

    'aliases' => [
        'MingCrypt' => ShaoZeMing\LaravelCrypt\Facade\Crypt::class,   //This is default in laravel 5.5
    ],
```

### lumen

- 在 bootstrap/app.php 中 82 行左右：
```
$app->register( ShaoZeMing\LaravelCrypt\CryptServiceProvider::class);
```
将 `vendor/ShaoZeMing/laravel-crypt/config/crypt.php` 拷贝到项目根目录`/config`目录下，并将文件名改成`crypt.php`。

### configuration 

```php
// config/crypt.php

    
    /**
     * 本项目的app_secret
     */
    'app_secret' =>env('XTHK_APP_SECRET','12345678912345678912345678912312'),

    /**
     * 加密规则,支持AES-128-CBC，AES-256-CBC
     */
    'cipher' => env('XTHK_CIPHER','AES-256-CBC'),


```


## Usage


```php
use Crypt;

//第1种
$result = MingCrypt::::crypt('你知道我对你不仅仅是喜欢');
print_r($result);




```


Example:

```php
$data = ['test'=>123];
$sign = MingCrypt::sign($data);   //签名
print_r($sign);
$check = MingCrypt::signCheck($data,$sign);   //延签
print_r($check);

$payload =  MingCrypt::encrypt($data);  //加密
print_r($payload);
$data = MingCrypt::decrypt($payload);   //解密
print_r($data);

```

## License

MIT

