# Laravel Sproc

[![Latest Version on Packagist](https://img.shields.io/packagist/v/masterei/laravel-sproc.svg?style=flat-square)](https://packagist.org/packages/masterei/laravel-sproc)
[![GitHub Tests Action Status](https://img.shields.io/github/workflow/status/masterei/laravel-sproc/run-tests?label=tests)](https://github.com/masterei/laravel-sproc/actions?query=workflow%3Arun-tests+branch%3Amain)
[![GitHub Code Style Action Status](https://img.shields.io/github/workflow/status/masterei/laravel-sproc/Check%20&%20fix%20styling?label=code%20style)](https://github.com/masterei/laravel-sproc/actions?query=workflow%3A"Check+%26+fix+styling"+branch%3Amain)
[![Total Downloads](https://img.shields.io/packagist/dt/masterei/laravel-sproc.svg?style=flat-square)](https://packagist.org/packages/masterei/laravel-sproc)

Laravel Query Builder for handling a stored procedure.

## Installation

You can install the package via composer:

```bash
composer require masterei/laravel-sproc
```

Optionally, you can publish the config file with:

```bash
php artisan vendor:publish --tag="sproc-config"
```

## Usage

Retrieving data:

```php
use Masterei\Sproc\Facades\SP;

 /**
 * execute()
 * Use this method if you are not expecting any dataset result.
 * @return boolean
 */

SP::call('stored_procedure_name')
    ->params([
        'Param01' => 'Arg01',
        'Param02' => 'Arg02',
    ])
    ->execute();


/**
 * get()
 * Standard way of retrieving data from stored procedure.
 * This method accepts a dataset index. The default index is 0.
 */

SP::call('stored_procedure_name')
    ->params([
        'Param01' => 'Arg01',
        'Param02' => 'Arg02',
    ])
    ->get();


/**
 * first()
 * Returns first object from an object array.
 */

SP::call('stored_procedure_name')
    ->params([
        'Param01' => 'Arg01',
        'Param02' => 'Arg02',
    ])
    ->first();


/**
 * all()
 * Retrieves all dataset result.
 * Can be chained with first() method.
 */

SP::call('stored_procedure_name')
    ->params([
        'Param01' => 'Arg01',
        'Param02' => 'Arg02',
    ])
    ->all();


/**
 * fetch()
 * Use this method to initialize dataset results.
 * Can be chained with first(), get() or all() method.
 */

$sp = SP::call('stored_procedure_name')
    ->params([
        'Param01' => 'Arg01',
        'Param02' => 'Arg02',
    ])
    ->fetch();

// example
$data01 = $sp->get(1);
$data02 = $sp->get(2);


/**
 * getLastInsertedId()
 * Returns id, ID or first row results generated by a stored procedure.
 * Use this after execute() method.
 */

SP::call('stored_procedure_name')
    ->params([
        'Param01' => 'Arg01',
        'Param02' => 'Arg02',
    ])
    ->execute()
    ->getLastInsertedId();
```

## Note
- This package uses Laravel Eloquent Collection meaning that you can freely use its features like groupBy(), sortBy(), map() etc.

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
