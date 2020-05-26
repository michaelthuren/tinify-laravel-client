# Tinify Laravel 6+ Client
Tinify API support for Laravel 6+

## Install

``` bash
$ composer require michaelthuren/tinyfy-laravel-client
```

Add this to your config/app.php, 

under "providers":
```php
        michaelthuren\tinyfy-laravel-client\TinifyLaravelServiceProvider::class,
```
under "aliases":

```php
        'Tinify' => michaelthuren\tinyfy-laravel-client\Facades\Tinify::class
```


And set a env variable `TINIFY_APIKEY` with your TinyPNG API key.

If you want to directly upload the image to `aws s3`, you need set the env variables of following with your aws s3 credentials.

```php
    S3_KEY=
    S3_SECRET=
    S3_REGION=
    S3_BUCKET=
```

## Examples

```php
	$result = Tinify::fromFile('\path\to\file');


	$result = Tinify::fromBuffer($source_data);

	$result = Tinify::fromUrl($image_url);

	/** To save as File **/
	$result->toFile('\path\to\save');

	/** To get image as data **/
	$data = $result->toBuffer();
```

```php

	$s3_result = Tinify::fileToS3('\path\to\file', $s3_bucket_name, '/path/to/save/in/bucket');

	$s3_result = Tinify::bufferToS3($source_data, $s3_bucket_name, '/path/to/save/in/bucket');

	$s3_result = Tinify::urlToS3($image_url, $s3_bucket_name, '/path/to/save/in/bucket');

	/** To get the url of saved image **/
	$s3_image_url = $s3_result->location();
	$s3_image_width = $s3_result->width();
	$s3_image_hight = $s3_result->height();

```

`NOTE:` All the images directly save to s3 is publicably readable. And you can set permissions for s3 bucket folder in your aws console to make sure the privacy of images.
