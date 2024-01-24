---
key:     core.server-session
title:   Server & Session
section: Core Modules
nav:
  prev:
    page: core.crown
    icon: prev
    name: Schedule (Crown)
  next:
    page: core.storage
    icon: next
    name: Storage
---

# ->>  Server & Session <<-

<div class="card card-body" markdown="1">
Embark upon a journey where the realms of the server and session are your domains to command.
The Server and Session modules serve as your loyal companions in navigating the server-environment and
session-state waters. Through the gateway `C`, access these singleton sentinels by 
invoking `C::Server()->...` and `C::Session()->...`. Traverse the server variables and session 
data with eloquence, using the dot notation to delve into nested realms,
making `get('bar.baz')` your key to `$_SERVER['bar']['baz']` and `$_SESSION['bar']['baz']`.
</div>

## ->> Server Module

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/server.jpg" alt="Server" /></div>

The Server module is your protocol droid, interpreting and presenting server variables (`$_SERVER`) at your behest.

### -> Public Methods

| Method | Syntax | Description | Return Type |
|--------|--------|-------------|-------------|
| get | `get(string $key, mixed $default = null): mixed` | Retrieves a server variable. | mixed |
| has | `has(string $key): bool` | Checks the existence of a server variable. | bool |
| getAll | `getAll(): array` | Retrieves all server variables. | array |

### -> Examples

```php
// Retrieving a server variable:
$serverName = C::Server()->get('SERVER_NAME');

// Checking the existence of a server variable:
$hasRemoteAddr = C::Server()->has('REMOTE_ADDR');

// Retrieving all server variables:
$allServerVars = C::Server()->getAll();
```

</div>

## ->> Session Module

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/session.jpg" alt="Session" /></div>

The Session module, your trusted session manager, ensures seamless session state 
maintenance across your galactic endeavors.

This gives you convenient access to `$_SESSION`.

It also handles the creation of a new session on this framework's init process.

### -> Public Methods

| Method           | Syntax                                    | Description                                                     | Return Type |
|------------------|-------------------------------------------|-----------------------------------------------------------------|-------------|
| destroy          | `destroy()`                               | Destroys the current session.                                   | bool        |
| refresh          | `refresh()`                               | Refreshes the current session.                                  | bool        |
| get              | `get(string $key, mixed $default = null)` | Retrieves a session value.                                      | mixed       |
| has              | `has(string $key)`                        | Checks if a session value exists.                               | bool        |
| set              | `set(string $key, mixed $value)`          | Sets a session value.                                           | void        |
| delete           | `delete(string $key)`                     | Deletes a session value.                                        | void        |
| checkFingerprint | `checkFingerprint()`                      | Validates the browser fingerprint to prevent session hijacking. | bool        |
| all              | `all()`                                   | Retrieves all session data.                                     | array       |

### -> Examples

```php
// Destroying the current session:
$sessionDestroyed = C::Session()->destroy();

// Refreshing the current session:
$sessionRefreshed = C::Session()->refresh();

// Retrieving, setting, and deleting a session value:
$sessionId = C::Session()->get('session_id');
C::Session()->set('session_id', 'new_value');
C::Session()->delete('session_id');

// Validating the browser fingerprint:
$fingerprintValid = C::Session()->checkFingerprint();

// Retrieving all session data:
$allSessionData = C::Session()->all();
```

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

With the Server and Session modules at your disposal, you possess the keys to the 
kingdom of server and session management. Whether interrogating server variables or 
preserving session state, these modules are your steadfast allies. Mastering their methods,
you unlock the doors to robust, secure, and intuitive interaction with the server
environment and session state, propelling your applications through the stars.

</div>
