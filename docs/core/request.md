---
key:     core.request
title:   Request
section: Core Modules
nav:
  prev:
    page: core.bbq
    icon: next
    name: Queue (BBQ)
  next:
    page: core.crown
    icon: next
    name: Schedule (Crown)
---

# ->>  Working with Requests <<-

<div class="card card-body" markdown="1">
In the realm of web development, adept handling of client requests is akin to the command bridge 
of a galactic cruiser, receiving and processing myriad signals to navigate through the digital cosmos.
The `Request` module in our framework is the epitome of such a command center, diligently managing 
the HTTP requests' input values — be it `$_GET`, `$_POST`, `$_REQUEST` parameters, 
JSON bodies or files uploaded from far-off client stations. 
Embrace the `Request` module as your trusted helmsman, facilitating smooth communication between the 
outer web universe and your application's core logic.



This module, like the loyal droids serving alongside, is available as a singleton instance. 
Its methods can be summoned via `C::Request()->...`, where `C` is the gateway to the singleton instances
of all modules within our framework.
</div>

## ->> Core Methods

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/request1.jpg" alt="Request Droid 1" /></div>

The below elucidation ventures through the significant methods offered by the `Request` module, complete with illustrative examples to guide you through the stars.

### -> `get($key, $default = null)`

Retrieves the value associated with a specified key from GET or POST parameters. The eloquence of dot notation is supported, simplifying your quest for nested parameters.

```php
// To access $foo['bar']['baz'], employ the following syntax:
$value = C::Request()->get('bar.baz');

// Should the key not exist, a default value can be specified:
$value = C::Request()->get('nonexistent.key', 'default_value');
```

### -> `has($key)`

Checks the presence of a specified key within the GET or POST parameters.

```php
// Examining the existence of 'bar.baz':
$exists = C::Request()->has('bar.baz');
```

To check for files you can use `hasFile($key)`.

### -> `getAll()`

Harvests all GET and POST parameters, returning them as an associative array.

```php
// Harvesting all available data:
$data = C::Request()->all();
```

### -> `getFile($key)`

Retrieves the uploaded file associated with a specified key.

This will return an `UploadedFile` object.

```php
// Fetching an uploaded star chart:
$starChart = C::Request()->getFile('star_chart');
```

</div>

## ->> All available Methods

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/request2.jpg" alt="Request Droid 2" /></div>

| Method               | Syntax                                                                                                                                                                    | Description                                           | Return Type                                           |
|----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|-------------------------------------------------------|
| get                  | `get(string $key, $default = null, $sanitize = false): mixed`                                                                                                             | Retrieves a request value.                            | mixed                                                 |
| has                  | `has(string $key): bool`                                                                                                                                                  | Checks if a key exists in the request.                | bool                                                  |
| set                  | `set(string $key, mixed $value): bool`                                                                                                                                    | Sets a request value.                                 | bool                                                  |
| setIfEmpty           | `setIfEmpty(string $key, mixed $value): bool`                                                                                                                             | Sets a request value if it's not set yet or empty.    | bool                                                  |
| getMultiple          | `getMultiple(array $keys): array`                                                                                                                                         | Retrieves multiple fields at once in an array.        | array                                                 |
| getAll               | `getAll(): array`                                                                                                                                                         | Gets all passed values as an array.                   | array                                                 |
| getAllPost           | `getAllPost(): array`                                                                                                                                                     | Gets all POST data.                                   | array                                                 |
| getAllGet            | `getAllGet(): array`                                                                                                                                                      | Gets all GET data.                                    | array                                                 |
| getHeader            | `getHeader(string $key, $default = null): ?string`                                                                                                                        | Gets a specific header value.                         | ?string                                               |
| gotUpload            | `gotUpload(string $name): bool`                                                                                                                                           | Checks if a file was uploaded successfully.           | bool                                                  |
| hasFile              | `hasFile(string $name): bool`                                                                                                                                             | Alias for `gotUpload`.                                | bool                                                  |
| getFile              | `getFile(string $name): bool                                                                                                                                              | UploadedFile`                                         | Retrieves an uploaded file.                           | bool/UploadedFile |
| saveFile             | `saveFile(string $name, string $destination, bool $override = true): bool`                                                                                                | Saves an uploaded file.                               | bool                                                  |
| saveAndResizeImage   | `saveAndResizeImage(string $name, string $destination, bool $override = true, int $width = 1920, string $mime = "image/jpeg", int $quality = 90): bool`                   | Saves and resizes/compresses an image.                | bool                                                  |
| saveImageAsThumbnail | `saveImageAsThumbnail(string $name, string $destination, bool $override = true, int $width = 600, int $height = 0, string $mime = "image/jpeg", int $quality = 80): bool` | Saves an image as a thumbnail (cropped).              | bool                                                  |
| getFiles             | `getFiles(string $name): UploadedFile[]`                                                                                                                                  | Retrieves multiple uploaded files.                    | array of UploadedFile                                 |
| getIpAddress         | `getIpAddress(): string`                                                                                                                                                  | Gets the IP address of the current request.           | string                                                |
| isHttpsRequest       | `isHttpsRequest(): bool`                                                                                                                                                  | Checks if the current request is via HTTPS.           | bool                                                  |
| accepts              | `accepts(string $str): bool`                                                                                                                                              | Checks if the browser accepts a certain content type. | bool                                                  |
| saveAllInSession     | `saveAllInSession(): void`                                                                                                                                                | Saves all request input values in session.            | void                                                  |
| getAllFromSession    | `getAllFromSession(): array                                                                                                                                               | bool`                                                 | Retrieves all request input values stored in session. | array/bool |

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">
The `Request` module is your trusted co-pilot, managing the crucial data 
transmitted via client requests. With its assortment of methods, navigating 
through the input parameters becomes a voyage of ease and precision.
The source code of this module, the blueprint of our digital cruiser, 
is available for your perusal and a deeper understanding 
[here](https://raw.githubusercontent.com/neoground/charm/master/src/Vivid/Kernel/Modules/Request.php). 
Engage with the `Request` module, and ensure your application sails smoothly through the galaxy of web development.

</div>
