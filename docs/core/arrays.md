---
key:     core.arrays
title:   Arrays
section: Core Modules
nav:
  prev:
    page: core.appstorage
    icon: prev
    name: App Storage
  next:
    page: core.bob
    icon: next
    name: Bob CLI
---

# ->> Arrays <<-

<div class="card card-body" markdown="1">
The Arrays module in the framework serves as a reservoir of handy array helper methods, 
simplifying and accelerating the manipulation of arrays in your projects.
</div>

## ->> Available Methods

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/array.jpg" alt="Section header image" /></div>

Below is an outline of the available public methods within the Arrays module:

- `has(array $arr, mixed $key): bool`: Checks if an array has a non-empty value by key. The key supports the usual dot-notation for sub-arrays.
- `get(array $arr, mixed $key, mixed $default = null): mixed`: Retrieves a specific value from an array. The key supports the usual dot-notation for sub-arrays.
- `getLastElement(array $arr): mixed`: Gets the last element of an array without removing it.
- `array_merge_recursive(array &$array1, array &$array2): array`: Merges two arrays recursively without duplicated entries.
- `sortByTwoKeys(array &$arr, mixed $key1, mixed $key2, string $order = 'desc'): void`: Sorts an array by two sub-array values.
- `hasDuplicates(array $array): bool`: Checks if an array has duplicates.

</div>

## ->> Array Collections

<div class="card card-body" markdown="1">

For more advanced tasks on arrays we provide Array Collections.

Laravel Collections, an elegant wrapper around arrays with a multitude of handy methods, significantly 
streamline array data manipulation. Similarly, the Array Collection within our framework, built 
upon Laravel Collections, offers a rich set of functionalities for array manipulation. 
You can utilize methods from Laravel Collections on our Array Collection.

Example:

```php
$arr = ['Foo', 'Bar', 'Baz'];
$arraycollection = C::Arrays()->from($arr);
$arraycollection->contains('Bar'); // true
```

Leverage the full breadth of Laravel Collections' methods as outlined in 
the [official documentation](https://laravel.com/docs/10.x/collections) to enrich your array 
manipulation capabilities within the framework.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

The Arrays module, coupled with the robust Array Collection, empowers developers with a suite of
tools for efficient array manipulation, embodying a blend of simplicity, efficiency, and the 
richness of functionalities carried over from Laravel Collections.

</div>
