---
key:     core.formatter
title:   Formatter
section: Core Modules
nav:
  prev:
    page: core.events
    icon: prev
    name: Events
  next:
    page: core.guard
    icon: next
    name: Guard & Token
---

# ->>  Formatter <<-

<div class="card card-body" markdown="1">
The Formatter module in Charm serves as a beacon of order amidst the vast ocean of raw, unstructured data.
As developers traverse through the realms of applications, they often encounter values in a form not 
suited for the end user's gaze. This module, with its arsenal of formatting methods, casts a structured 
spell upon these values, morphing them into a friendly guise. Whether it's a date crying out for a simple 
attire, or a string yearning for a sanitized existence, the Formatter heeds their call, bestowing upon 
them the desired facade.
</div>

## ->> Available Formatters

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/formatter.jpg" alt="Section title image" /></div>

### -> Date Specific Formatters

The input dates can be in any format which [Carbon](https://carbon.nesbot.com/docs/) 
(a very good date library we highly recommend) can parse. 
This is usually every standard format of date or date time.

| Method                                    | Description                                                                                 | Example                                      |
|-------------------------------------------|---------------------------------------------------------------------------------------------|----------------------------------------------|
| `formatDate($data)`                       | Formats a date in a long format specified in `main.yaml` (e.g. 4th April 2024).             | `formatDateShort('2023-10-07')`              |
| `formatDateShort($data)`                  | Formats a date in a short format specified in `main.yaml` (e.g. 4/20/24).                   | `formatDateShort('2023-10-07')`              |
| `formatDateTimeShort($data)`              | Formats a date with time in a short format specified in `main.yaml` (e.g. 20 Apr 24 16:20). | `formatDateTimeShort('2023-10-07 15:30:00')` |
| `formatDateDiff($date, $date_after_days)` | Formats a date as a human-readable difference (e.g., 3 months ago).                         | `formatDateDiff('2023-07-07', 365)`          |

### -> Number Formatters

| Method                                               | Description                                                                                                                                          | Example                      |
|------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| `formatNumber($no, $decimals, $decimal, $thousands)` | Formats a number for displaying, e.g. a price. You can manually set the separator characters. By default the ones specified in `main.yaml` are used. | `formatNumber(1337.42)`      |
| `removeTrailingZeros($no)`                           | Removes trailing zeros from a number.                                                                                                                | `removeTrailingZeros(8.00)`  |
| `formatBytes($bytes, $precision)`                    | Formats bytes to B/KB/MB/GB/... Returns a string like "1,8 MB".                                                                                      | `formatBytes(1024)`          |
| `percentageChange($old_price, $new_price)`           | Gets the percentage difference between two numbers (the amount the number has changed).                                                              | `percentageChange(100, 150)` |

### -> String and URL Formatters

| Method                  | Description                                        | Example                               |
|-------------------------|----------------------------------------------------|---------------------------------------|
| `sanitizeEmail($input)` | Sanitizes an email.                                | `sanitizeEmail('example@domain.com')` |
| `sanitizeUrl($input)`   | Sanitizes a URL.                                   | `sanitizeUrl('https://example.com')`  |
| `slugify($text)`        | Slugifies a text string. Perfect for URL creation. | `slugify('Hello World!')`             |

### -> Language Methods

Easy access for translation and language detection. You can configure the available languages and
the default language in your app's `main.yaml` - "session" section.

| Method                             | Description                                                         | Example                                          |
|------------------------------------|---------------------------------------------------------------------|--------------------------------------------------|
| `getLanguage()`                    | Gets the language name string for translation (e.g., "en" or "de"). | `getLanguage()`                                  |
| `setLanguage($lang)`               | Sets the language manually.                                         | `setLanguage('de')`                              |
| `setAutoLanguage()`                | Automatically sets language based on request detection.             | `setAutoLanguage()`                              |
| `translate($key, $vars, $default)` | Translates a text string.                                           | `translate('main:greeting', ['name' => 'Luke'])` |

Translations are simple text files at `app/Config/Lang/$lang`, where `$lang` is the language string, e.g. "en".

Each language can contain multiple `yaml` config files, it works just like the main config.

In our example `translate('main:greeting', ['name' => 'Luke'])` as an English visitor, we would look at
`app/Config/Lang/en/main.yaml` which should have an entry `greeting: Hello, {name}!`. This would then return
`Hello, Luke!`.


</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

In the grand tapestry of application development, presenting data in a manner that
resonates with the end user's comprehension is a quest of its own. The Formatter module
stands as a loyal companion in this quest, offering a bouquet of formatting solutions. 
With a simple invocation, dates, numbers, and strings are adorned with a mantle of readability,
while the mystical lands of URLs and Emails are navigated with a sanitized touch. As you tread
further into the Charm framework, the Formatter module remains an indispensable ally, ensuring
every value is presented with grace and precision, bridging the chasm between raw data and user-friendly presentation.

</div>
