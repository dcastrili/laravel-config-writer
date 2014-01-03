## Laravel Config Writer

Write to Laravel Config files and maintain file integrity.

This library is an extension of the Config component used by Laravel. It adds the ability to write to configuration files.

You can rewrite array values inside a basic configuration file that returns a single array definition (like a Laravel config file) whilst maintaining the file integrity, leaving comments and advanced settings intact.

The following value types are supported for writing: strings, integers and booleans.

### Usage Instructions

Swap out the `config` IoC object:

```php
App::instance('config', function($app){
    $loader = $app->getConfigLoader();
    $writer = October\Rain\Config\FileWriter($loader, $app['path'].'/config');
    return new October\Rain\Config\Repository($loader, $writer, $app['env']);
})
```

You can now write to config files:

```
Config::write('app.url', 'http://octobercms.com');
```

### Usage outside Laravel

The `Rewrite` class can be used anywhere.

```php
$writeConfig = new October\Rain\Config\Rewrite;
$writeConfig->toFile('path/to/config.php', [
    'item' => 'new value',
    'nested.config.item' => 'value'
]);
```