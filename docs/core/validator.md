---
key:     core.validator
title:   Validator
section: Core Modules
nav:
  prev:
    page: core.storage
    icon: prev
    name: Storage
  next:
    page: routing.overview
    icon: next
    name: Routing - Overview
---

# ->>  Validator <<-

<div class="card card-body" markdown="1">
In the realms of code, validation is the silent guardian, the watchful protector that ensures order 
amidst the chaos of data influx. The Validator module, a vigilant sentinel, stands ready to scrutinize 
the data, ensuring it adheres to the established laws of your digital dominion. Access this bastion 
of validation via `C::Validator()->...`, and let no errant data trespass unchallenged.
</div>

## ->> Built-in Validation Functions

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/validate1.jpg" alt="Section header image" /></div>

The Validator module is equipped with a cadre of built-in functions forged to battle common 
validation adversaries. Here are some of them illustrated:

```php
$isValidEmail = C::Validator()->validateEmail('test@example.com');
$isValidURL = C::Validator()->validateUrl('https://example.com');
```

You can use these built-in methods, each returning true or false, depending if the value is valid or not:

| Description               | Method                                             |
|---------------------------|----------------------------------------------------|
| Validate an email address | `validateEmail($email)`                            |
| Validate a domain         | `validateDomain($domain)`                          |
| Validate a mac address    | `validateMacAddress($mac)`                         |
| Validate a URL            | `validateUrl($url, $pathRequired, $queryRequired)` |

</div>

## ->> Extending the Validation Arsenal with Respect-Validator

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/validate2.jpg" alt="Section header image" /></div>

Beyond the built-in arsenal, the Validator module allies with the formidable Respect-Validation, 
expanding its validation repertoire to over 150 validations. Summon this 
ally with `C::Validator()->create()`, and command its extensive validation powers as illustrated below:

```php
// Extended validation:
$isValid = C::Validator()->create()
    ->dateTime()
    ->between(new DateTime('yesterday'), new DateTime('tomorrow'))
    ->validate(new DateTime('now'));  // true

C::Validator()->create()->stringVal()->between('a', 'f')->validate('d'); // true
```

Discover more about the Respect-Validator and its expansive 
validation armory in its [documentation](https://respect-validation.readthedocs.io/en/latest/).

Since Respect-Validation is installed as a package you can also use it directly if you want to.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

The Validator module is your steadfast companion in maintaining the integrity of your application's data.
With its built-in validation functions, it valiantly guards against common validation adversaries. 
When the battle demands an extended validation arsenal, the Respect-Validator awaits your command, 
ready to validate with valor. Engage with the Validator module, and ensure that no errant data breaches 
the sanctity of your digital dominion.

</div>
