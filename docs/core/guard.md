---
key:     core.guard
title:   Guard & Token
section: Core Modules
nav:
  prev:
    page: core.formatter
    icon: prev
    name: Formatter
  next:
    page: core.http
    icon: next
    name: HTTP
---

# ->> Guard & Token <<-

<div class="card card-body" markdown="1">
The Charm framework provides two modules, Guard and Token, 
that help secure and manage authentication and authorization in web applications. 
The Guard module is responsible for handling user authentication and authorization, 
while the Token module helps manage secure access tokens.

The Guard module provides a simple login and logout system, 
with auto login, auto logout, and route filters to secure routes from unauthorized access.
It also provides user authentication, password hashing, and modern security features. 
Guard helps ensure that only authenticated users can access the necessary routes and resources.

The Token module, on the other hand, helps manage secure access tokens, 
which can be used for authentication and authorization purposes.
It provides functionality for generating tokens, saving them, and verifying them during usage. 
Token helps provide secure access to resources or services, without the need for re-authentication.

In this documentation, we will cover the different features, methods, 
and usage examples of the Guard and Token modules. By the end of this documentation, 
you will be able to integrate and use these modules in your own web application
to provide secure authentication and authorization.
</div>

## ->> Guard <<-

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/guard.jpg" alt="Section title image" /></div>

The Guard module provides a secure and easy-to-use authentication system
for your PHP application. With features like auto-login, auto-logout, 
simple login and logout handling, and route filters for checking authentication, 
you can be sure that your application is secure and reliable.

### -> Built-in features

#### Auto-login if remember me cookie is set

The Guard module provides an automatic login feature if the "remember me" cookie is set.
This cookie is set for a period of time, and if the cookie contains valid data, 
the user gets automatically logged in.

#### Auto-logout of expired sessions

To ensure that your users are logged out when their session has expired, 
the Guard module provides an auto-logout feature. 
This feature checks if the user's session has expired and logs them out automatically.

#### Login throttling and logging

Too many logins trigger a dynamic throttling for the tried user account,
but also for the accessing client.

Wrong login attempts are saved in redis. The access to the login can be
restricted after a specific amount of tries.

### -> Configuration

You can easily configure the Guard module in the `main.yaml` config file:

```yaml
# ---------------------------------------------------------------------------
# :: Guard auth system
# ---------------------------------------------------------------------------
guard:
  # Enable auth system (guard)?
  enabled: true
  # User class with namespace to use for authentication
  user_class: 'App\Models\User'
  # Column in database where username is stored
  username_field: email
  # Location of API token. Can be field of user table or full path to Token class
  token_location: 'App\Models\Token'
  # The master password for all logins (false for disabling)
  master_password: false
  # Unique authentication salt
  auth_salt: 'Set-this-to-a-secret-salt-value'
  # The route to redirect to in case of no auth
  no_auth_route: login
```

### -> Easy login and logout

The Guard module provides simple and easy-to-use methods for handling logins and logouts. These methods take care of all the necessary authentication checks and redirect the user accordingly.

Example:

```php
if (C::Guard()->login('gordonfreeman', 'Hl3C0nfirmed!')) {
    // login successful
} else {
    // login failed
}

// Logout
C::Guard()->logout();
```

### -> Route filter `guard:auth` which checks auth

The Guard module provides a route filter called "guard:auth" which checks if the 
user is logged in before allowing access to the specified route. 
If the user is not logged in, they are redirected to the route specified in the
config at `main:guard.no_auth_route`.

```php
#[Route("GET", "/secret", "secret", "guard:auth")]
public function secret()
{
    // code for secret page
}
```

### -> Example controller

Here's an example controller using the Charm Guard auth system.

```php
<?php
namespace App\Controllers;

use App\Models\User;
use Charm\Vivid\C;
use Charm\Vivid\Controller;
use Charm\Vivid\Kernel\Output\Redirect;
use Charm\Vivid\Kernel\Output\View;
use Charm\Vivid\Router\Attributes\Route;

class AuthController extends Controller
{
    /**
     * Show login page
     *
     * @return View
     */
    #[Route("GET", "/login", "login")]
    public function getLogin(): View
    {
        return View::make('auth.login')->with([
            'title' => 'Login'
        ]);
    }

    /**
     * Handle login (form submit)
     *
     * @return Redirect
     */
    #[Route("POST", "/login", "dologin")]
    public function doLogin(): Redirect
    {
        // Get username and password from form
        $username = C::Request()->get('email');
        $password = C::Request()->get('password');
        $rememberme = C::Request()->get('remember', false);

        // Get amount of wrong login attempts of current IP
        $amount = C::Guard()->getWrongLoginAttempts();
        if ($amount > 20) {
            // Block this attempt
            return $this->loginError('Blocked');
        }

        // Find user by username
        $user = C::Guard()->findUserByUsername($username);

        // User found?
        if (!is_object($user)) {
            return $this->loginError('User Not Found', true);
        }

        // Check password
        if (C::Guard()->checkPassword($username, $password)) {
            // Login successful
            C::Guard()->handleLogin($user, $rememberme);
            return Redirect::to('dashboard');
        }

        return $this->loginError('Wrong Credentials');
    }

    /**
     * Handle login error redirection
     *
     * @param string $message redirect message
     * @param bool   $attempt save attempt?
     *
     * @return Redirect
     *
     */
    private function loginError(string $message, bool $attempt = false): Redirect
    {
        if ($attempt) {
            // Save wrong login attempt
            C::Guard()->saveWrongLoginAttempt();
        }

        // Redirect
        return Redirect::to('login')->withMessage($message);
    }

    /**
     * Do the logout, redirect to login page
     *
     * @return Redirect
     */
    #[Route("GET", "/logout", "logout", "guard:auth")]
    public function getLogout(): Redirect
    {
        C::Guard()->logout();
        return Redirect::to('login')->withMessage('Thanks for your visit!');
    }
}
```

</div>

## ->> Token <<-

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/token.jpg" alt="Section title image" /></div>

The Token class is a module in the Charm PHP framework for managing tokens and user authentication. 
This class provides a variety of methods for working with tokens, including generating, setting, 
and retrieving them, as well as checking for authentication and finding users based on their tokens.
Basic Usage

To get started, you can simply access all token methods via the magic magnet:

```php
use Charm\Vivid\C;
$token = C::Token()->createToken();
```
You can have a single token per user in an own column. If your `User` model 
has a column `api_token`, your `main.yaml` would include:

```yaml
guard:
  token_location: 'api_token'
```

Or you use the built-in `Token` model, which is more flexible 
(you can also use your own, simply change the path to the class):

```yaml
guard:
  token_location: 'App\Models\Token'
```

### -> Generating a Token

To generate a token, you can use the createToken() method. 
This method takes an optional argument for the number of bytes to use in the token, 
and an optional argument for whether the token is an API token.

```php
$tokenString = C::Token()->createToken(32, true);
```

This will generate a new API token with 32 bytes and return the resulting string.

### -> Setting a Token

You can manually set a token using the setToken() method. This can be useful for 
testing purposes or for cases where you want to set a specific token.

```php
C::Token()->setToken("mynewtoken");
```

This will set the token to "mynewtoken". Please note that this will change the token 
for all subsequent code executed after this command.

### -> Retrieving a Token

You can retrieve the token using the getToken() method. If no token is found, 
the method will return false.

```php
$tokenString = C::Token()->getToken();
```

This will return the token string, or false if no token is found.

### -> Checking for a Token

You can check if a token is present using the hasToken() method.

```php
if (C::Token()->hasToken()) {
    // do something
}
```

This will return true if a token is present, and false otherwise.

### -> Finding a User by Token

You can find a user based on their token using the findUserByToken() method. 
This will return the user object if found, or false if no user is found.

```php
$user = C::Token()->findUserByToken();
if ($user) {
    // do something
}
```

### -> Getting the User

You can retrieve the user based on the token using the getUser() method. 
This will return the user object or the system user if no user is found.

```php
$user = C::Token()->getUser();
```

### -> Checking for Authentication

You can check if a user is authenticated by calling the isLoggedIn() method.

```php
if (C::Token()->isLoggedIn()) {
    // do something
}
```

</div>

## ->> Client token

<div class="card card-body" markdown="1">

The `client_token` property is used to handle client-specific tokens that 
can be provided along with the user token. This can be useful when you have a 
web application with multiple clients or when you have a mobile application 
that needs to authenticate with your API.

The client token is stored in the `client_token` property and can be retrieved 
using the `getClientToken()` method. 
You can check whether a client token has been provided by calling `hasClientToken()`.

You can set the client token using the `setClientToken()` method. 
This method takes one argument, the client token value.

Example:

```php
// Set the client token
C::Token()->setClientToken('my_client_token');

// Check whether a client token has been provided
if (C::Token()->hasClientToken()) {
    // Do something with the client token
}

// Get the client token value
$clientToken = C::Token()->getClientToken();
```

You can easily validate the client token in a middleware.

</div>

## ->> Making a request

<div class="card card-body" markdown="1">

To send the token as an HTTP header, you can use the `Authorization` header. 
If this somehow doesn't work or isn't allowed,
you can also use the `X-Authorization` header instead.

Here's an example for user token only:

```php
use Charm\Vivid\C;

$response = C::Http()->get('https://example.com/api', [
    'headers' => [
        'Authorization' => 'Bearer my_user_token'
    ]
]);
```

If you want to use the same structure as in the next example, 
you can also set the `Authorization` header to: `usertoken="my_user_token"`

And another one sending user and client (app specific) token:

```php
use Charm\Vivid\C;

$response = C::Http()->get('https://example.com/api', [
    'headers' => [
        'Authorization' => 'usertoken="my_user_token" client="my_client_token"'
    ]
]);
```

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">
The Token class is a powerful tool for managing tokens and user authentication 
in your Charm PHP applications. With its flexible and powerful set of methods,
you can easily generate, set, retrieve, and manage tokens, 
making it easy to build secure, authenticated applications.
</div>
