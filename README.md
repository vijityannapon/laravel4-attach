## File upload with resized.

Attach is a file uploader for Laravel version 4.

### Installation

- [Attach on Packagist](https://packagist.org/packages/teepluss/attach)
- [Attach on GitHub](https://github.com/teepluss/laravel4-attach.git)

To get the lastest version of Theme simply require it in your `composer.json` file.

~~~
"teepluss/attach": "dev-master"
~~~

You'll then need to run `composer install` to download it and have the autoloader updated.

Once Attach is installed you need to register the service provider with the application. Open up `app/config/app.php` and find the `providers` key.

~~~
'providers' => array(

    'Teepluss\Attach\AttachServiceProvider'

)
~~~

Attach also ships with a facade which provides the static syntax for creating collections. You can register the facade in the `aliases` key of your `app/config/app.php` file.

~~~
'aliases' => array(

    'Theme' => 'Teepluss\Attach\Facades\Attach'

)
~~~

Publish config using artisan CLI.

~~~
php artisan config:publish teepluss/attach
~~~

## Usage

Basic upload
~~~php
$attach = Attach::inject(array(
    'subpath' => 'tee'
))
->add(Input::file('userfile'))
->upload();

var_dump($attach->onComplete());
~~~

Remote upload
~~~php
$attach = Attach::inject(array(
    'remote' => true
))
->add('http://...../file.png')
->upload();
~~~

Resizing
~~~php
$attach = Attach::open('/path/to/image.png')->resize();

// To specific scales from config.

$attach = Attach::open('/path/to/image.png')->resize(array('l', 'm'));
~~~

Upload and Resize
~~~php
$attach = Attach::add(Input::file('userfile'))->upload()->resize();
~~~

Remove
~~~php
$attach = Attach::open($path)->remove();
~~~

You can inject your config anytime
~~~php
$attach = Attach::inject(array(
    ..... YOUR CONFIG .....
))
->upload();
~~~

Callback
~~~php
Attach::inject(array(

    'onUpload' => function($result)
    {
        //
    },

    'onComplete' => function($results)
    {
        //
    },

    'onRemove' => function($result)
    {
        //
    }

))
->upload()
->resize();
~~~

## Support or Contact

If you have some problem, Contact teepluss@gmail.com

[![Alt Buy me a beer](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](
https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=admin%40jquerytips%2ecom&lc=US&item_name=Teepluss&no_note=0&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donateCC_LG%2egif%3aNonHostedGuest)