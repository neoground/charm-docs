---
key:     core.storage
title:   Storage
section: Core Modules
nav:
  prev:
    page: core.server-session
    icon: prev
    name: Server & Session
  next:
    page: core.validator
    icon: next
    name: Validator
---

# ->>  Storage <<-

<div class="card card-body" markdown="1">
In the vast cosmos of digital domain, managing the delicate fabric of data, be it localized or distant, 
is an endeavor of critical significance. The Storage module emerges as your dependable conduit 
to navigate through the manifold avenues of file storage, both local and remote, ensuring a 
seamless symbiosis between your application and the data it cradles. Access this module via 
the cosmic gateway `C::Storage()->...`, and venture into the realm of file storage with precision and ease.
</div>

## ->> Working with Local Files Manually

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/storage1.jpg" alt="Section header image" /></div>

In the quest of mastering the digital realm, engaging with the local file system is a fundamental endeavor. 
This section unveils a suite of methods designed to provide a streamlined interface for manual 
interactions with local files, nested within the web space. The methods are bifurcated into two
categories: one aiding in the discovery and organization of paths, and the other facilitating easy
handling of directories and files. Embark on this segment of the journey with a structured approach
to local file management.

### -> Methods for Paths

| Method        | Syntax                           | Description                                                         |
|---------------|----------------------------------|---------------------------------------------------------------------|
| getAppPath    | `getAppPath(): string`           | Retrieves the absolute path to "app" directory.                     |
| getAssetsPath | `getAssetsPath(): string`        | Retrieves the absolute path to "assets" directory.                  |
| getBasePath   | `getBasePath(): string`          | Retrieves the absolute path to app's base directory.                |
| getVarPath    | `getVarPath(): string`           | Retrieves the absolute path to "var" directory.                     |
| getLogPath    | `getLogPath(): string`           | Retrieves the absolute path to "var/logs" directory.                |
| getCachePath  | `getCachePath(): string`         | Retrieves the absolute path to "var/cache" directory.               |
| getDataPath   | `getDataPath(): string`          | Retrieves the absolute path to "data" directory.                    |
| getModulePath | `getModulePath($module): string` | Retrieves the absolute path to base directory of a specific module. |

### -> Methods for Easy Handling

| Method                         | Syntax                                                                 | Description                                                                                      |
|--------------------------------|------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| createDirectoriesIfNotExisting | `createDirectoriesIfNotExisting(string $path, int $mode = 0777): bool` | Ensures the existence of directories along the specified path, creating them if necessary.       |
| deleteFileIfExists             | `deleteFileIfExists(string $file) : bool`                              | Deletes a file if it exists.                                                                     |
| pathToUrl                      | `pathToUrl(string $path): string`                                      | Converts an absolute path to a URL (only applicable for paths within app's directory structure). |
| urlToPath                      | `urlToPath(string $url): string`                                       | Converts a URL to an absolute path (only applicable for paths within app's directory structure). |
| scanDir                        | `scanDir($path, int $sorting_order = 0): array                         | false`                                                                                           | Retrieves all files and directories within a specified directory, excluding "." and "..".              |

</div>

## ->> Using the Filesystem API

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/storage2.jpg" alt="Section header image" /></div>

Leverage the Filesystem API to engage with the `data` and `var` directories effortlessly.
Extend its realm to custom directories or FTP/SFTP storages, and interact with the 
Filesystem instances as dictated by the 
[Flysystem documentation](https://flysystem.thephpleague.com/docs/usage/filesystem-api/), which this is based on.

```php
$content = json_encode($my_data);

try {
    C::Storage()->get('data')->write('/exports/example.json', $content);
} catch (FilesystemError | UnableToWriteFile $exception) {
    // Handle error
}

// ...

try {
    $response = C::Storage()->get('data')->read('/exports/example.json');
    $content = json_decode($response);
} catch (FilesystemError | UnableToReadFile $exception) {
    // handle the error
}
```

### -> Adding Storages

Elevate your storage capabilities by defining additional storage configurations in your `app/Config/main.yaml`.

Here are some example storages:

```yaml
storages:
  mycustomdir:
    type: 'local'
    path: '/mnt/data/mycustomdir'
  myftp:
    type: 'ftp'
    host: 'example.com'
    username: 'example_user'
    password: 'Duk3Nuk3m!'
    port: 21
  mysftp:
    type: 'sftp'
    host: 'example.com'
    username: 'foo'
    password: 'bar'
```

Access these storages via `C::Storage()->get($name);`. Valid storage names in this 
example are: `data`, `var`, `mycustomdir`, `myftp`, `mysftp`.

</div>

## ->> Working with images

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/storage3.jpg" alt="Section header image" /></div>

In a digital cosmos adorned with multimedia, images often emerge as the quintessence of user interaction and engagement. Whether it's crafting a vibrant profile avatar or accommodating a myriad of user uploads, managing images with adeptness is pivotal. Charm extends its embrace to the realm of image manipulation through the integration of the renowned `claviska/SimpleImage` class, encapsulated within Charm's own Image class.

### -> Image Manipulation

Charm's Image class, a descendant of SimpleImage, inherits the bounty of image manipulation methods SimpleImage affords, thereby enabling a streamlined and potent handling of images within your application.

Consider an instance where an uploaded image is to be resized to the dimensions of 250x250 pixels and saved as a JPEG image; the following code snippet elucidates this process:

```php
$uid = C::Guard()->getUserId();
$file = C::Request()->getFile('avatar');
if($file) {
    $img = new Image()->fromFile($file)
                      ->autoOrient()
                      ->thumbnail(250, 250);

    C::Storage()->get('data')
                ->write('users/' . $uid . '/avatar.jpg',
                        $img->toString('image/jpeg', 75));
}
```

In this illustration, an image uploaded through a form is acquired, resized, and stored within the data storage under a user-specific directory, all with a few succinct lines of code.

### -> Discover More with SimpleImage

Dive deeper into the vast ocean of image manipulation possibilities with SimpleImage. Explore the array of methods it provides for a multitude of image operations including, but not limited to, resizing, cropping, color adjustments, and much more.

Explore the [SimpleImage repository](https://github.com/claviska/SimpleImage) to unveil the extensive capabilities it brings to the table.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

With the Storage module as your companion, traverse the intricate pathways of file storage, 
be it local or remote, with ease and precision. The methods and configurations it provides
empower you to handle files and directories meticulously, ensuring a harmonious interplay 
between your application and the data it interacts with.

With the addition of image handling capabilities, the Storage module further solidifies 
its standing as a robust and comprehensive solution for managing a wide spectrum of file
storage and manipulation tasks. The amalgamation of SimpleImage's prowess with Charm's
elegant design provides a seamless and powerful medium for image processing, thereby enriching
the user experience and facilitating a more vibrant and interactive application landscape.

</div>
