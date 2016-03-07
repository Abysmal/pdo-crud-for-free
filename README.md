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

``` php

// file: /src/Product.php
class Product extends \Mattsmithdev\Pdo\DatabaseTable {
    // private properties with EXACTLY same names as DB table columns
    
    // and ensure DB table has 'id' integer auto-increment primary key
}
```

``` php

// file: /public-web/index.php or /src/SomeController->method()

// get all products from DB as array of Product objects
$products = Product::getAll();

// outputs something like: 
//  hammer, nail, nuts, bolts
foreach ($products as $product){
    print $product->getDescription() . ' ,';
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
