---
key:     start.magnet
title:   Magic Magnet
section: Getting Started
nav:
  prev:
    page: start.mvc
    icon: prev
    name: Models, Views & Controllers
  next:
    page: core.overview
    icon: next
    name: Core Modules - Overview
---

# ->> Usage of C:: - The Magic Magnet <<-

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/start/magnet.jpg" alt="The Magic Magnet" /></div>

Welcome to the interstellar journey of understanding and utilizing the magic magnet `C::` in Charm. 
This framework, much like the harmony and charm of a galaxy, thrives on the principle of singleton instances.

In the vast expanse of the Charm universe, `C::`, like a trusty astromech droid, offers you an effortless
way to access and manage all loaded modules of the framework. This guide will equip you with the 
knowledge to harness the full potential of `C::`, enhancing your voyage through the Charm cosmos.
</div>

## ->> Working with C:: - Your Astromech Droid

<div class="card card-body" markdown="1">
Navigating the galaxy of Charm can be a breeze with your astromech droid, `C::`. To interact with it, 
make sure to `use Charm\Vivid\C;`.

Start your exploration by calling `C::` in your IDE. Just like a star map, if your code completion is 
accurate and Charm is available via composer, a galaxy of modules will unfurl before your eyes.

Use `C::` to access any module by its name, such as the built-in `C::Formatter()->...`. 
If you have a custom module aptly named as a green planet, say `Naboo`, you can summon it by `C::Naboo()->...`.

```php
use Charm\Vivid\C;
$input = C::Request()->get('term');
```

Above, we are using `C::` to access the `Request` module and retrieve the input query parameter `term`.

### --> The Charm:: Alias

Should you encounter any disturbances in the force using the short `C::`, you have an ally in `Charm::`.
It's the exact same access, albeit with a different name. In this case, the force you need to wield
is `Charm\Vivid\Charm;`.

```php
use Charm\Vivid\Charm;
$data = Charm::Request()->get('data');
```

Here, we use `Charm::` as an alias for `C::` to access the `Request` module and fetch the data.

### --> Checking Module Availability

Ever wondered if a particular module is within your reach or if it's in a galaxy far, far away? 
The force provides you with `Charm::has('ModuleName')`. This will return a boolean indicating 
the availability of the module.

```php
if (Charm::has('DeathStar')) {
    // Death Star module is available, proceed with operation
} else {
    // Abort mission!
}
```

### --> The Core Modules

In every galaxy, there are celestial bodies that are always present. Similarly, the base modules 
are always available in Charm. Refer to the [Core Modules section](*BASEURL*/docs/charm/core.overview) 
in this documentation for an in-depth exploration of these modules.

### --> Graceful Shutdown

In the event that you must stop your app, remember the Jedi way and do not resort to `die()` or `exit()`. 
Instead, use `C::shutdown()`, a graceful way to call all shutdown hooks and clean up the environment / session.

```php
// This is not the way
// die();

// This is the way
C::shutdown();
```

This method ensures that all operations are wrapped up neatly and the system environment is left in a 
clean state, just like leaving no trace when a Jedi disappears into the Force.

That concludes our journey of understanding the `C::` - the magic magnet of Charm. May the `C::`
be with you as you explore the rest of the Charm galaxy!
</div>