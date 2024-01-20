---
key:     core.http
title:   HTTP
section: Core Modules
nav:
  prev:
    page: core.guard
    icon: prev
    name: Guard & Token
  next:
    page: core.logging
    icon: next
    name: Logging
---

# ->>  HTTP Module <<-

<div class="card card-body" markdown="1">
In the vast galaxy of web development, where the Force — both Light and Dark — governs the destiny 
of your applications, Charm's built-in HTTP Module serves as your lightsaber, allowing you to wield the
formidable powers of HTTP requests with precision and agility. Built upon the renowned 
[Guzzle](https://docs.guzzlephp.org/en/stable/index.html) package, 
this module offers a robust interface to perform various HTTP methods while also supporting all 
the Guzzle features. Our mantra is simple: to make your journey from Padawan to Master as seamless as possible.
</div>

## ->> Methods and Examples

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/datacenter1.jpg" alt="Structure" /></div>

All the methods in the HTTP module can be accessed using the `C::Http()->...` syntax.
Let's delve into the available methods:

### -> Get

Invoke an HTTP GET request.

It returns a `HttpResponse` (see below) or throws an Exception if the request  didn't succeed.

The options are passed to Guzzle, so you can use all
[Guzzle Request Options](https://docs.guzzlephp.org/en/stable/request-options.html).

```php
get(string $url, array $options = []): HttpResponse
```

**Example:**

```php
$response = C::Http()->get('https://api.example.com/users', ['headers' => ['Authorization' => 'Bearer token']]);
echo $response->getBody();
```

### -> Delete

Execute an HTTP DELETE request to remove a resource.

It returns a `HttpResponse` (see below) or throws an Exception if the request  didn't succeed.

The options are passed to Guzzle, so you can use all
[Guzzle Request Options](https://docs.guzzlephp.org/en/stable/request-options.html).

```php
delete(string $url, array $options = []): HttpResponse
```

**Example:**

```php
$response = C::Http()->delete('https://api.example.com/users/1');
echo $response->getStatusCode();  // Should return 204 for successful deletion
```

### -> Head

Make a HEAD request, which is similar to GET but without the response body.

It returns a `HttpResponse` (see below) or throws an Exception if the request  didn't succeed.

The options are passed to Guzzle, so you can use all
[Guzzle Request Options](https://docs.guzzlephp.org/en/stable/request-options.html).

```php
head(string $url, array $options = []): HttpResponse
```

**Example:**

```php
$response = C::Http()->head('https://api.example.com/users');
$headers = $response->getHeaders();
```

### -> Options

Invoke an OPTIONS request to discover available methods for a resource.

It returns a `HttpResponse` (see below) or throws an Exception if the request  didn't succeed.

The options are passed to Guzzle, so you can use all
[Guzzle Request Options](https://docs.guzzlephp.org/en/stable/request-options.html).

```php
options(string $url, array $options = []): HttpResponse
```

**Example:**

```php
$response = C::Http()->options('https://api.example.com/users');
```

### -> Patch

Use PATCH to apply partial modifications to a resource.

It returns a `HttpResponse` (see below) or throws an Exception if the request  didn't succeed.

The options are passed to Guzzle, so you can use all
[Guzzle Request Options](https://docs.guzzlephp.org/en/stable/request-options.html).

```php
patch(string $url, array $options = []): HttpResponse
```

**Example:**

```php
$response = C::Http()->patch('https://api.example.com/users/1', ['json' => ['name' => 'NewName']]);
```

### -> Post

Execute a POST request to create a new resource.

It returns a `HttpResponse` (see below) or throws an Exception if the request  didn't succeed.

The options are passed to Guzzle, so you can use all
[Guzzle Request Options](https://docs.guzzlephp.org/en/stable/request-options.html).

```php
post(string $url, array $options = []): HttpResponse
```

**Example:**

```php
$response = C::Http()->post('https://api.example.com/users', ['json' => ['name' => 'John']]);
```

### -> Put

Use PUT to update a resource or create it if it doesn't exist.

It returns a `HttpResponse` (see below) or throws an Exception if the request  didn't succeed.

The options are passed to Guzzle, so you can use all
[Guzzle Request Options](https://docs.guzzlephp.org/en/stable/request-options.html).

```php
put(string $url, array $options = []): HttpResponse
```

**Example:**

```php
$response = C::Http()->put('https://api.example.com/users/1', ['json' => ['name' => 'John']]);
```

### -> Get a new Client

Generate a new Guzzle client with optional configurations.

```php
getNewClient(array $config = []): Client
```

**Example:**

```php
$newClient = C::Http()->getNewClient(['base_uri' => 'https://newapi.example.com']);
```

</div>

## ->> Response Methods

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/datacenter2.jpg" alt="Structure" /></div>

Every HttpResponse object you receive from all request specific methods has several utility functions:

| Description                          | Method                         | Response Type       |
|--------------------------------------|--------------------------------|---------------------|
| Get the whole body string            | `getBody()`                    | `string`            |
| Get the status code of the response  | `getStatusCode()`              | `int`               |
| Get the JSON body as array or object | `getJsonBody($asarray = true)` | `array` or `object` |
| Get all response headers             | `getHeaders()`                 | `array`             |
| Get a specific response header       | `getHeader(string $name)`      | `array`             |
| Get the whole guzzle response object | `getGuzzleResponse()`          | `ResponseInterface` |

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

The HTTP Module in Charm is not just another cog in the machine; it is the Kyber crystal at 
the core of your development lightsaber. It gives you not just the tools but also the agility
to engage with the Force — be it RESTful APIs, third-party integrations, or any other 
HTTP-enabled data source. So go ahead, young Padawan, may the source be with you!

</div>
