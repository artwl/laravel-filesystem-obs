[![packagist](https://badgen.net/packagist/v/artwl/laravel-filesystem-obs?icon=github)](https://packagist.org/packages/artwl/laravel-filesystem-obs) [![](https://badgen.net/packagist/php/artwl/laravel-filesystem-obs)](https://packagist.org/packages/artwl/laravel-filesystem-obs) [![](https://badgen.net/packagist/name/artwl/laravel-filesystem-obs?icon=github)](https://packagist.org/packages/artwl/laravel-filesystem-obs) [![](https://badgen.net/packagist/license/artwl/laravel-filesystem-obs)](https://packagist.org/packages/artwl/laravel-filesystem-obs) 

# Huawei Cloud OBS for Laravel

Huawei Cloud OBS storage for Laravel based on [artwl/laravel-filesystem-obs](https://github.com/artwl/laravel-filesystem-obs).

# Requirement

- PHP >= 7.1.3 || PHP >= 8.0

# Installation

```shell
$ composer require "artwl/laravel-filesystem-obs:v3.4.0"
```

注：需要composer为2.0及以上版本

# Configuration

1. After installing the library, register the `Obs\ObsServiceProvider` in your `config/app.php` file:

  ```php
  'providers' => [
      // Other service providers...
      Obs\ObsServiceProvider::class,
  ],
  ```

2. Add a new disk to your `config/filesystems.php` config:
 ```php
 <?php

 return [
    'disks' => [
        //...
        'obs' => [
            'driver' => 'obs',
            'key' => env('OBS_ACCESS_ID'), // <Your Huawei OBS AccessKeyId>
            'secret' => env('OBS_ACCESS_KEY'), // <Your Huawei OBS AccessKeySecret>
            'bucket' => env('OBS_BUCKET'), // <OBS bucket name>
            'endpoint' => env('OBS_ENDPOINT'), // <the endpoint of OBS, E.g: (https:// or http://).obs.cn-east-2.myhuaweicloud.com | custom domain, E.g:img.abc.com> OBS 外网节点或自定义外部域名
            'cdn_domain' => env('OBS_CDN_DOMAIN'), //<CDN domain, cdn域名> 如果isCName为true, getUrl会判断cdnDomain是否设定来决定返回的url，如果cdnDomain未设置，则使用endpoint来生成url，否则使用cdn
            'ssl_verify' => env('OBS_SSL_VERIFY'), // <true|false> true to use 'https://' and false to use 'http://'. default is false,
            'debug' => env('APP_DEBUG'), // <true|false>
        ],
        //...
     ]
 ];
 ```

# Usage

```php
$disk = Storage::disk('obs');

// create a file
$disk->put('avatars/filename.jpg', $fileContents);

// check if a file exists
$exists = $disk->has('file.jpg');

// get timestamp
$time = $disk->lastModified('file1.jpg');
$time = $disk->getTimestamp('file1.jpg');

// copy a file
$disk->copy('old/file1.jpg', 'new/file1.jpg');

// move a file
$disk->move('old/file1.jpg', 'new/file1.jpg');

// get file contents
$contents = $disk->read('folder/my_file.txt');

// fetch url content
$file = $disk->fetch('folder/save_as.txt', $fromUrl);

// get file url
$url = $disk->getUrl('folder/my_file.txt');

// get file upload token
$token = $disk->getUploadToken('folder/my_file.txt');
$token = $disk->getUploadToken('folder/my_file.txt', 3600);

// get private url
$url = $disk->privateDownloadUrl('folder/my_file.txt');
```

[Full API documentation.](http://flysystem.thephpleague.com/api/)

# License

MIT
