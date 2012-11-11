# Laravel Twig - Laravel View Replacement

Laravel Twig is a clone of [TwigView](https://github.com/akhawaja/TwigView) which replaces the default Laravel View class with the 
[Twig Template Engine](http://twig.sensiolabs.org/).

We use [Composer](http://getcomposer.org/) and the [composer bundle](http://bundles.laravel.com/bundle/composer) 
to fetch the Twig library.

##Install Composer
Install composer inside your project directory

	curl -s http://getcomposer.org/installer | php

Create a **composer.json** file at the root of your project
  
	{
	    "require": {
	        "php": ">=5.3.0",
	        "twig/twig": "1.11.*"
	    }
	}

Install your composer packages, which will install the Twig library files in your **vendor/** directory.

	php composer.phar install  


## Install the Twig bundle

	php artisan bundle:install twig

That should install the **composer** bundle as well since its a dependancy.

In the **application/bundles.php** file, register the Composer and Twig bundles.

```php
return array(
	'composer' => array('auto' => true),
	'twigview' => array(
    'location' => 'twig', 'autoloads' => array(
        'map' => array(
            'TwigView\\View' => '(:bundle)/view.php',
        	)
    	)
    ),
);
```

### Replace the View alias (optional)

In the *application/config/application.php* file, replace the alias with the following:

```php
'aliases' => array(
    ...
    'View' => 'TwigView\\View',
);
```

If you leave the alias as-is, you can still call ```\TwigView\View``` in your controllers.

## Usage ##

All your views must have the **.twig** file extension. You can use the ```TwigView\View``` object in the same 
manner as the ```Laravel\View``` object. Just keep in mind that you are using Twig syntax inside your views.

For example call the Twig view like this

```php
$data = array('message' => 'Hello');
return \TwigView\View::make('home.index', $data);
``` 

If you aliased TwigView you can do this

```php
$data = array('message' => 'Hello');
return View::make('home.index', $data);
``` 

and in your **home/index.twig** do this

	{{ message }}


##Upgrading

To upgrade change the Twig version to in the **composer.json** file at the root of your project
  
	{
	    "require": {
	        "php": ">=5.3.0",
	        "twig/twig": "1.11.*" 
	    }
	}

Update using Composer

	php composer.phar update  


## License ##

Copyright (c) 2012 Amir Khawaja

This software is provided 'as-is', without any express or implied warranty. In no event will the 
author be held liable for any damages arising from the use of this software.

Permission is granted to anyone to use this software for any purpose, including commercial 
applications, and to alter it and redistribute it freely, subject to the following restrictions:

- The origin of this software must not be misrepresented; you must not claim that you wrote the original software. 
If you use this software in a product, an acknowledgment in the product documentation would be appreciated 
but is not required.
- Altered source versions must be plainly marked as such, and must not be misrepresented as being the original software.
- This notice may not be removed or altered from any source distribution.

## Thanks ##

A special thank you to @michaelenger of [mustacheview](https://github.com/michaelenger/mustacheview) for the 
inspiration.