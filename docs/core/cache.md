---
key:     core.cache
title:   Cache
section: Core Modules
nav:
  prev:
    page: core.bob
    icon: prev
    name: Bob CLI
  next:
    page: core.confdebug
    icon: next
    name: Config & Debug
---

# ->> Cache <<-

<div class="card card-body" markdown="1">
The Cache module, an embodiment of simplicity and efficiency, is meticulously engineered to be a PSR-compliant caching mechanism, offering a temporary abode for any kind of data. Currently, it employs Redis as its storage sentinel, safeguarding your data against the tempest of redundant operations. As we traverse further along the corridors of innovation, plans are afoot to diversify the storage mediums to include flat files, Memcache, and databases.

A built-in console command, `bob cache:clear`, stands guard to clear internal caches, though the auto-expiration feature ensures a seamless cleanup post the specified duration. Thus, manual intervention in cache cleanup is rendered obsolete.

Accessing the Cache module is an exercise in familiarity, with the syntax `C::Cache()->...` ushering you into its realm.
</div>

## ->> Working with the Cache

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/brain.jpg" alt="Section header image" /></div>

### -> Remember data

The `remember` method is your loyal companion in data retrieval and storage. It seeks to fetch the data from cache if it's already nestled there; if not, it diligently stores the data in the cache, post a routine data operation.

```php
C::Cache()->remember('MyKey', 120, function() {
    $data = getDataDoStuff();
    return $data;
});
```

Here, 'MyKey' is the unique identifier, 120 is the time in minutes the data shall remain
in cache, and the function is the method of data retrieval. This simple invocation ensures 
that for a span of 120 minutes, the data, once cached, is swiftly retrieved, minimizing the operational load.

### -> Advanced remembering with CacheEntry

For those seeking a deeper communion with the cache, the `CacheEntry` class beckons.
It offers a sophisticated mechanism to handle data, enveloping it with tags that act as beacons 
for future reference or deletion.

```php
$ce = new CacheEntry('MyKey');
$ce->setTags(['tag1', 'tag2'])
   ->setValue(function() {
        $data = getDataDoStuff();
        return $data;
   });
C::Cache()->setEntry($ce, 120);
```

By setting tags, you are essentially creating a dynamic pathway to manage datasets in your cache. 
This feature allows for a more nuanced control over data deletion, especially when certain tags 
are to be expunged from the cache realm.

### -> Check & Get data from the Cache

**Retrieve all keys of cache entries with a specific tag:**

`C::Cache()->getByTag($tag)`

Parameter: `$tag`: Cache tag or array of cache tags.

**Get a specific stored cache entry:** 

`C::Cache()->get($key, $default = null)`

Parameters: `$key`: Cache key, `$default`: Default return value if entry not found (optional).

**Check if a cache key exists:**

`C::Cache()->has($key)`

Parameter: `$key`: The key to check.

### -> Remove data from the Cache

**Remove a single cache entry:**

`C::Cache()->remove($key)`

Parameter: `$key`: The key to remove.

### -> Remove data by tag from the Cache

`C::Cache()->removeByTag($tag)`

Parameter: `$tag`: Cache tag or array of cache tags.

</div>

## ->> Clearing Charm's Cache

<div class="card card-body" markdown="1">

A vigilant overseer, the `bob cache:clear` command is your go-to mantra for clearing internal caches. Though, with the auto-expiration feature at play, manual cleanup is seldom necessitated. This is mainly used if you want to clear charm's internal caches - of routes, views and so on.

```bash
bob cache:clear
```

A simple invocation of this command sweeps clean the internal caches, maintaining the hygiene and efficiency of your cache module.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

The Cache module is a testament to how simplicity and efficiency can coalesce to form a robust foundation for data management. As you venture into the depths of caching with the Cache module, you are not just storing data, but embracing a culture of optimized data handling, ensuring your digital endeavors are always a leap ahead in performance. The future beckons with the promise of more storage mediums, further broadening the horizons of what's possible with Neoground's Cache module.

</div>
