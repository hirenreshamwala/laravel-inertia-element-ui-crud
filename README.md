# element-ui crud generator

[![Latest Version on Packagist](https://img.shields.io/packagist/v/xt/laravel-inertia-element-ui-crud.svg?style=flat-square)](https://packagist.org/packages/xt/laravel-inertia-element-ui-crud)
[![Total Downloads](https://img.shields.io/packagist/dt/xt/laravel-inertia-element-ui-crud.svg?style=flat-square)](https://packagist.org/packages/xt/laravel-inertia-element-ui-crud)

Generate CRUD for Element-UI (Vue 3) and Inertia Js.

This package will generate files to perform CRUD, based on the database table schema. It will generate all the fields in list, create and update form pages.

[Vue Plugin](https://www.npmjs.com/package/laravel-inertia-element-ui-crud-vue3)

## Features
- Generate list, create and update view pages
- Generate controller which perform insert, update and delete
- Generate form for all the fillable fields defined in model file
- Server side validation (required and maximum length) 

## Installation

You can install the package via composer:

```bash
composer require xt/laravel-inertia-element-ui-crud
```

Install npm package:

```bash
npm install laravel-inertia-element-ui-crud-vue3 --save
```

## Add code

add following function to the app/Http/Controllers/Controller.php

```php
function filterOrderParameters(){
    $sort_order = \request('order', 'd');
    if ($sort_order == ''){
        $sort_order = 'd';
    }
    if ($sort_order == 'a'){
        $sort_order = 'asc';
    } else {
        $sort_order = 'desc';
    }
    return $sort_order;
}
```

## Usage

Add following code to the boot method of the app/Providers/AppServiceProvider.php

```php
Inertia::share('flash', function () {
    return [
        'message' => Session::get('message'),
    ];
});

Inertia::share([
    'success' => function () {
        return Session::get('success')
            ? Session::get('success')
            : '';
    },
]);

Inertia::share([
    'error' => function () {
        return Session::get('error')
            ? Session::get('error')
            : '';
    },
]);

Inertia::share([
    'errors' => function () {
        return Session::get('errors')
            ? Session::get('errors')->getBag('default')->getMessages()
            : (object) [];
    },
]);
```

## Command to generate CRUD

```bash
php artisan crud:generator <ControllerName> <ModelName>
```

Prepare model before generate crud

make sure controller name without including controller for example `User` which generates `UserController`

Example:
```bash
#This will generator view file for Jetstream

php artisan crud:generator User User
```
or
```bash
#This will generator view file for breeze

php artisan crud:generator User User --template=breeze
```


### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

### Security

If you discover any security related issues, please email hiren.reshamwala@gmail.com instead of using the issue tracker.

## Credits

-   [Hiren Reshamwala](https://github.com/hirenreshamwala)
-   [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
