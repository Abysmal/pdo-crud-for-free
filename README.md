# pdo-crud-for-free

[![Latest Version on Packagist][ico-version]][link-packagist]
[![Software License][ico-license]](LICENSE.md)
[![Build Status][ico-travis]][link-travis]
[![Coverage Status][ico-scrutinizer]][link-scrutinizer]
[![Quality Score][ico-code-quality]][link-code-quality]
[![Total Downloads][ico-downloads]][link-downloads]

This package provides a few classes to try to give programmers using PDO in a simple way some instance CRUD (create-read-update-delete) method, 'for free', simply by subclassing \Mattsmithdev\Pdo\DatabaseTable.

All code is (intented :-) to follow PSR-1, PSR-2 coding standards. Classes are following the PSR-4 autoloading standard.

## Install

Via Composer

``` bash
$ composer require mattsmithdev/pdo-crud-for-free
```

NOTE - until I get the hang of SemVer (and get to a 1.0.0 or later version), 
then you'll need to force the dev-master download as follows:

``` bash
$ composer require mattsmithdev/pdo-crud-for-free=dev-master
```



## Usage

This example assumes you have a MySQL DB table named 'products', with columns 'id' and 'description'. You need to write a corresponding class 'Product' (note capital first letter ...).

``` php

// file: /src/Product.php
namespace <MyNameSpace>;

class Product extends \Mattsmithdev\PdoCrud\DatabaseTable 
{
    // private properties with EXACTLY same names as DB table columns
    
    // and ensure DB table has 'id' integer auto-increment primary key
}
```

``` php

// file: /public-web/index.php or /src/SomeController->method()

require_once __DIR__ . '/<PATH_TO_AUTLOAD>';

// the DatabaseManager class needs the following 4 constants to be defined in order to create the DB connection
define('DB_HOST', '<host>');
define('DB_USER', '<db_username>');
define('DB_PASS', '<db_userpassword>');
define('DB_NAME', '<db_name>');

// get all products from DB as array of Product objects
$products = \<MyNameSpace>\Product::getAll();

// outputs something like:
//  hammer, nail, nuts, bolts
foreach ($products as $product){
    print $product->getDescription() . ', ';
}
```

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

``` bash
$ composer test
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) and [CONDUCT](CONDUCT.md) for details.

## Security

If you discover any security related issues, please email dr_matt_smith@me.com instead of using the issue tracker.

## Credits

- [Matt Smith][https://github.com/dr-matt-smith]

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

[ico-version]: https://img.shields.io/packagist/v/mattsmithdev/:package_name.svg?style=flat-square
[ico-license]: https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square
[ico-travis]: https://img.shields.io/travis/mattsmithdev/:package_name/master.svg?style=flat-square
[ico-scrutinizer]: https://img.shields.io/scrutinizer/coverage/g/mattsmithdev/:package_name.svg?style=flat-square
[ico-code-quality]: https://img.shields.io/scrutinizer/g/mattsmithdev/:package_name.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/mattsmithdev/:package_name.svg?style=flat-square

[link-packagist]: https://packagist.org/packages/mattsmithdev/:package_name
[link-travis]: https://travis-ci.org/mattsmithdev/:package_name
[link-scrutinizer]: https://scrutinizer-ci.com/g/mattsmithdev/:package_name/code-structure
[link-code-quality]: https://scrutinizer-ci.com/g/mattsmithdev/:package_name
[link-downloads]: https://packagist.org/packages/mattsmithdev/:package_name
[link-author]: https://github.com/mattsmithdev
[link-contributors]: ../../contributors
