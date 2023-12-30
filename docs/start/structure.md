---
key:     start.structure
title:   Structure
section: Getting Started
nav:
  prev:
    page: start.installation
    icon: prev
    name: Installation
  next:
    page: start.mvc
    icon: next
    name: Models, Views & Controllers
---

# ->> Charm Structure: A Galactic Guide <<-

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/start/structure.jpg" alt="Structure" /></div>

In a galaxy not so far away, you've embarked on a journey to create a web application using the Charm PHP Framework. To
ensure your quest is successful, you must understand the structure of your project. Here, we'll explore the Charm
project structure and provide a brief overview of each folder's purpose.

```
├── app/
│  ├── Config/
│  │   ├── Environments/
│  │   ├── Lang/
│  │   ├── connections.yaml
│  │   ├── main.yaml
│  │   ├── modules.yaml
│  │   └── user.yaml
│  ├── Controllers/
│  ├── Jobs/
│  │   ├── Console/
│  │   └── Cron/
│  ├── Models/
│  ├── Routes/
│  ├── System/
│  │   ├── EventListener/
│  │   ├── Exceptions/
│  │   ├── Middleware/
│  │   ├── Migrations/
│  │   └── Traits/
│  ├── Views/
│  ├── app.env
│  └── Engine.php
├── assets/
├── data/
├── var/
├── vendor/
├── .gitignore
├── .htaccess
├── .composer.json
├── .composer.lock
├── index.php
├── LICENSE.md
├── nginx.conf
├── phpunit.xml
└── README.md
```

Let's dive deeper into the cosmic world of Charm project structure inside the `app` folder:

| File / Folder          | Purpose                                                  |
|------------------------|----------------------------------------------------------|
| `Config/`              | Configuration files                                      |
| `Config/Environments`  | Environment-specific configuration files                 |
| `Config/Lang`          | Language translation yaml files (i18n)                   |
| `Controllers/`         | Controllers                                              |
| `Jobs/Console`         | Console commands                                         |
| `Jobs/Cron`            | Cron jobs                                                |
| `Models/`              | Models                                                   |
| `Routes/`              | Routes                                                   |
| `System/EventListener` | Event listeners executed when an event is fired          |
| `System/Exceptions`    | Custom exceptions                                        |
| `System/Middleware`    | Middlewares, e.g., for authentication in routes          |
| `System/Migrations`    | Database migration (table creation) files                |
| `System/Traits`        | Traits                                                   |
| `Views/`               | Contains all Twig view files                             |
| `app.env`              | Contains the name of the environment to use (gitignored) |
| `Engine.php`           | Entry file for the Charm module "App"                    |

</div>

## ->> Embracing Modularity: The Galactic Approach

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/start/modular.jpg" alt="Modular" /></div>
In the vast universe of web development, the Charm PHP Framework stands out with its core principle: modularity. This
powerful concept allows developers to build flexible and scalable applications, much like the intricate interconnections
between the stars and planets of the galaxy.

### --> A Modular Core: The Vivid Nexus

At the heart of Charm lies the central core, Vivid. This celestial force holds everything together and registers each
module, making it available through the magic magnet. With Vivid, you can easily access any module within the system by
invoking

```php
C::Module()->method();
```

### --> Modular Building Blocks: Planetary Components

Charm's modular architecture ensures that every aspect of the framework is encapsulated within its own module. This
includes input data, custom classes (such as formatting), connections (like SQL or Redis), and internal structures like
AppStorage.

By embracing modularity, you can replace existing modules or integrate the best tools and libraries for your custom
projects. This approach allows you to create a truly tailored application, as unique as the celestial bodies that
inhabit the galaxy.

### --> Developing Your Own Constellations: Custom Modules

The Charm framework encourages you to create your own modules for different parts of your application. This modular
design enables you to build a plug-in system or streamline development in larger teams, fostering collaboration like the
gravitational pull between celestial bodies.

To integrate your custom modules, simply link them in the `app/modules.yaml` configuration file. With this approach, you
can easily extend your application's functionality and harness the full potential of Charm's modular architecture.

### --> Conclusion

By adopting the modular philosophy of the Charm PHP Framework, you can embark on a cosmic journey through web
development, creating flexible and scalable applications. With the power of modularity and the guiding light of the
Vivid core, your web applications will shine like the stars in the galaxy.
</div>