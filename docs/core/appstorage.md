---
key:     core.appstorage
title:   App Storage
section: Core Modules
nav:
  prev:
    page: core.overview
    icon: prev
    name: Overview
  next:
    page: core.arrays
    icon: next
    name: Arrays
---

# ->> AppStorage <<-

<div class="card card-body" markdown="1">
The AppStorage module is a dexterous in-memory storage mechanism, designed to house 
lightweight data in a singleton instance array. Its usage permeates the framework, 
providing a haven for internal data such as routing data and configuration values.
This philosophy of employing in-memory storage for often-needed, lightweight data,
fosters a realm of efficiency and swift data access.
</div>

## ->> Available Methods

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/brain2.jpg" alt="Section header image" /></div>

### -> General Storage Operations

You can store and fetch any kind of data in the AppStorage. Just keep in mind that the data is stored
in runtime in an array.

- `getAll()`: Fetches the entire storage; primarily for debugging or testing.
- `get($module, $key, $default = null)`: Retrieves a value from the AppStorage.
- `has($module, $key)`: Verifies the existence of a key.
- `set($module, $key, $value)`: Assigns a value in the AppStorage.
- `delete($module, $key)`: Extinguishes a value from the AppStorage.

### -> Array-Specific Operations

- `append($module, $key, $value)`: Adds a value to a pre-existing array or creates a new array if none exists.
- `aget($module, $arrname, $key, $default = null)`: Retrieves a value from an array in the AppStorage.
- `aset($module, $arrname, $key, $value)`: Sets a value in an array in the AppStorage.

### -> Cache Management

You usually don't need to use these methods - they're used internally for handling the AppStorage cache.
See the section below for easy usage via CLI.

- `clearCache()`: Empties the cache.
- `generateCache()`: Produces the cache and replaces the existing one.
- `loadInitStorage()`: Loads the cache into AppStorage.

</div>

## ->> CLI Commands

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/brain3.jpg" alt="Section header image" /></div>

### -> Cache the AppStorage

`php bob.php appstorage:generate`

Caches the AppStorage data available post system initialization to a file, 
thereby accelerating the framework's startup time as it merely loads the file and stands ready.

This shouldn't be used in development because this cache will override any file changes. But on
production systems this gives a great performance boost. It also clears the AppStorage cache
automatically if a file is already present.

### -> Clear the AppStorage cache

`php bob.php appstorage:clear`

Purges the generated AppStorage cache, paving the way for fresh data storage.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

The AppStorage module is a quintessence of how lightweight data management, when melded with an intuitive in-memory storage mechanism, can bolster the framework's performance and ease of data accessibility. The CLI commands and a plethora of methodical operations further exemplify the module's potential in orchestrating a well-organized data storage and retrieval system.

</div>
