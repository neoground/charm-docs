---
key:     core.confdebug
title:   Config & Debug
section: Core Modules
nav:
  prev:
    page: core.cache
    icon: prev
    name: Cache
  next:
    page: core.database
    icon: next
    name: Database
---

# ->> Configuration Guide <<-

<div class="card card-body" markdown="1">
Welcome, young Padawan, to the heart of the Charm Framework, 
where the secrets of the config files are stored. 
Just as the Jedi archives hold the knowledge of the galaxy, 
these files contain the essential information that shapes your 
web application's destiny. By mastering the art of configuration, 
you will bring balance to your project and achieve greatness.
</div>

## ->> Config Files Overview

<div class="card card-body" markdown="1">
These ancient scrolls guide your application, found at `app/Config`:

| Configuration File                           | Description                                                |
|----------------------------------------------|------------------------------------------------------------|
| `main.yaml`                                  | The core of your application's configuration               |
| `connections.yaml`                           | The hyperlanes connecting your app to various data sources |
| `user.yaml`                                  | The Holocron of personalized settings                      |
| `modules.yaml`                               | The blueprint for assembling additional modules            |
| Environment-specific configuration overrides | The Force that adapts your app to different situations     |
| Language/i18n files                          | The Galactic Compendium of translations                    |

</div>

## ->> Usage

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/conf2.jpg" alt="Section title image" /></div>

### Accessing Config Values

To access the wisdom contained within these files, use the power of the C class. Observe the following example:

```php
use Charm\Vivid\C;

$value = C::Config()->get('user:greetings.wise', 'Hello');
```

This will give you access to your local `user.yaml` config, which contains this:

```yaml
greetings:
  wise: May the Force be with you
```

If the value is not set, it returns `Hello`, the default value.

### -> Understanding Key Structure

The key structure is an essential aspect of the Charm Framework. 
Mastering this concept will empower you to easily access configuration 
values across your application and modules. Let's explore some examples to illuminate the way.

#### -> Module-specific configuration

```php
$value = C::Config()->get('MyModule#user:foo.bar');
```

This key accesses the `user.yaml` config file within the `MyModule` module, and retrieves the value of `foo -> bar`.

#### -> App's configuration

```php
$value = C::Config()->get('connections:database.hostname');
```

This key accesses the `connections.yaml` config file of the app, and retrieves the value of `database -> hostname`.

#### -> Nested values in configuration

You can nest your configuration as much as you want to, thanks to yaml free structure.

```php
$value = C::Config()->get('user:foo.bar.baz.abc.def');
```

This key accesses the `user.yaml` config file of the app, and retrieves the value of `foo -> bar -> baz -> abc -> def`.

### -> In Debug Mode

To check if your app is in debug mode, use the following method:

```php
$isDebug = C::Config()->inDebugMode();
```

This is a shorthand for `C::Config()->get('main:debug.enabled', false)`.

### -> Formatted Config Values

To retrieve a formatted value, use the getf method. This is especially useful for translations:

```php
$formattedValue = C::Config()->getf('main:greetings.wise', ['name' => 'Yoda'], $default);
```

This will return the value with vsprintf applied, using the provided array.

### -> Caching

On system init the configuration files are loaded into the AppStorage to minimize Disk I/O.
If you use `bob appstorage:generate` to cache the basic content,
this will include the environment specific configuration values, so the configuration is
available on the fly.
</div>

## ->> Environment-specific configuration

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/conf1.jpg" alt="Section title image" /></div>

In Charm Framework, managing environment-specific configurations is seamless. 
These configurations allow you to override specific values depending on the 
environment your application is running in, such as development, staging, or production.

The Environments folder contains environment-specific configurations. 
When the app environment is set to "Local" in `app/app.env`, the values 
in the corresponding environment configuration files will take precedence 
over the standard configuration values in the `app/Config` folder.

This environment specific folders are located at `app/Config/Environments`.

You can add a new environment using the "bob" CLI tool with the following command:

```sh
bob c:env
```

This command will create a new environment folder in the Environments directory and
set up a basic configuration, allowing you to override specific configuration
values for that environment.
</div>

## ->> Translations

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/conf4.jpg" alt="Section title image" /></div>

Charm Framework makes handling translations (i18n) straightforward. 
To retrieve a translated value, you can use the `C::Formatter()->translate()` method. 
The user's language is automatically detected, with the default value being set 
in the `main:local.shortlang` configuration.

For example, suppose the `Config/Lang/en/main.yaml` file contains the following:

```yaml
demo:
  hello: Hey {name}
```

You can access the translated value like this:

```php
C::Formatter()->translate('main:demo.hello', ['name' => 'Luke']);
```

This code snippet would output "Hey Luke". The `translate()` method uses 
the `C::Config()->getf()` method under the hood, which retrieves a 
formatted value by applying `vsprintf` with the provided array.

You can access it easily in any twig view:

```twig
<p>{{ __('main:demo.hello', {'name': 'Luke'}) }}</p>
```

By mastering environment-specific configurations and translations in 
the Charm Framework, you can create flexible, multilingual 
applications that adapt to different environments and user preferences.
</div>

## ->> Debug Mode

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/conf3.jpg" alt="Section title image" /></div>

The debug mode in the Charm Framework is designed to help developers
identify and fix issues in their applications more efficiently. 
When enabled in app/Config/main.yaml, the debug mode activates 
various features such as debug output, pretty exceptions (based on [filp/whoops](https://github.com/filp/whoops/)), 
debug logging, and more. Additionally, caching is disabled in debug mode.

### -> Pretty Exceptions

When debug mode is enabled, any exceptions or fatal errors thrown will
display a pretty exception page, providing you with additional information 
to help you resolve the issue. Error pages, such as error views or 
JSON responses, are disabled in debug mode. Instead, you'll always receive debug output.

### -> Debug Bar

In debug mode, all views include a debug bar at the bottom of the page. 
This bar displays executed queries, system messages, and other data,
such as the current route and user. The debug bar is built on [PHP Debug Bar](https://github.com/maximebf/php-debugbar),
and you can access all its methods using `C::DebugBar()->getInstance()`.

### -> Dump and Done

The "dump, die, done" function (or `ddd()`) is a handy debugging tool. 
To use it, simply call `ddd($var1, $var2, "Foobar");`. 
This function outputs the content of all variables using a user-friendly 
JavaScript GUI, making it easy to navigate through large arrays or objects. 
After dumping, the code will automatically stop. 
This is particularly useful for debugging more complex issues. 
If debug mode is disabled, `ddd();` will also be disabled.

This tool is based on [Kint](https://github.com/kint-php/kint), also providing
support in twig views based on [Kint-twig](https://github.com/kint-php/kint-twig).

### -> Dump and not Done

If you don't want to stop your script and just output the variable at some point,
use the `d()` command with the same syntax: `d($var1, $var2, "Foobar");`.
This will output the variable's content like `ddd()` does, but continue afterwards.

### -> Dump to Debug Bar

For non-fatal errors or situations where you'd like to inspect the content of some 
variables or data, you can dump the content to the debug bar. Usage is similar to `ddd()`: 
call `ddb($var1, $var2, "Foobar");`.

This won't stop your script and continue execution, just like `d()`.

The content will be found in the Messages tab of the debug bar. 
You can also manually add output to the debug bar message tab by using:

```php
Charm::DebugBar()->getInstance()['message']->info("FooBar");
```

This is useful if you want a different status than "debug".
</div>

## ->> Conclusion

<div class="card card-body" markdown="1">
Now, go forth, young Padawan, and harness the power of the Charm Framework configuration
to build web applications that will bring peace and prosperity to the galaxy.
May the Force be with you!
</div>
