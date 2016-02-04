## JetFire PSR-4 Autoloader

A PSR-4 autoloader.

### Installation

Via [composer](https://getcomposer.org)

```bash
composer require jetfirephp/autoload
```

### Usage

To use the autoloader, first instantiate it, then register it with SPL autoloader stack:

```php
require_once __DIR__ . '/vendor/autoload.php';

$loader = new \JetFire\Autoloader\Autoload();

$loader->register();
```

### Add Namespace

To add a single namespace here how to do this :

```php
$loader->addNamespace('App\Admin','/path/to/app-admin/src');
$loader->addNamespace('App\Admin','/path/to/app-admin/tests');
```

For multiple namespaces :

```php
$loader->setNamespaces([
    'App\Admin' => [
        '/path/to/app-admin/src',
        '/path/to/app-admin/tests'
    ],
    'App\Public' => '/path/to/app-public'
]);
// or
$loader->setNamespaces('/path/to/namespaces/file.php');
```

This will override all previous namespace settings.

### Add Class

To map a class to a file, use the `addClass()` method.

```php
$loader->addClass('App/Admin/Auth','/path/to/app-admin/Auth.php');
```

For multiple classes :

``php
$loader->setClassCollection([
    'App\Admin\Auth' => '/path/to/app-admin/Auth.php'
]);
// or
$loader->setClassCollection('path/to/classes/file.php');
```

### Smart Autoloader

If you set a default base directory for your autoloader like this :

```php
$loader = new \JetFire\Autoloader\Autoload('/path/to/base/directory');
```

And you want to instantiate a class `Auth.php` with the namespace `App\Admin` when you have not define this namespace in `addClass()` method, JetFire\Autoloader will check if the file `Auth.php` exists in `/path/to/base/directory/App/Admin/` folder. 