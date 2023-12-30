---
key:     start.installation
title:   Installation
section: Getting Started
nav:
  prev:
    page: index
    icon: prev
    name: Overview  
  next:
    page: start.structure
    icon: next
    name: Structure
---

# ->> Installation <<-

<div class="card card-body" markdown="1">
Join the Galactic Web Development Revolution!

Welcome, young Padawan, to the Charm Framework, an exceptional PHP web framework
that combines the power of the Force with the excitement
of the universe and its sci-fi versions. Our mission is to make web development an enjoyable
and artistic experience while providing top-notch performance and a professional toolkit.

To begin your journey, follow these simple steps to install the Charm Framework
and create your very first project in a galaxy far, far away.
</div>

## --> Requirements: Fuel for Your Galactic Adventure

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/start/serverracks.jpg" alt="Server Racks" /></div>
To ensure a smooth journey with the Charm Framework, make sure your system meets the following requirements:

- PHP 8.0 or later (8.1 / 8.2 preferred, ideally with Redis module)
- Composer
- Depending on your app:
    - Database: MariaDB, MySQL, SQLite, PostgreSQL or SQL Server
    - Redis
    - A web server, preferably nginx
</div>

## --> Installation: As Easy as the Kessel Run

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/start/bob.jpg" alt="Bob" /></div>
To install the Charm Framework, you first need to install Bob toolkit on your machine.

In a galaxy not so far away, Bob (short for Binary Operations Butler) was created
to serve as the ultimate command-line companion for Charm Framework developers.

Run the following command to install Bob:

```bash
curl -fSsL -o bob https://raw.githubusercontent.com/neoground/charm-toolkit/main/bob && chmod +x bob
sudo mv bob /usr/local/bin/bob
```

For more information on this, see the [Bob documentation](https://github.com/neoground/charm-toolkit).

Once installed, run the following command to create a new project:

```bash
bob new GalacticArchive
```

This command will generate a new project called `GalacticArchive` based on the [charm-wireframe](https://github.com/neoground/charm-wireframe) 
template and put it in the new created directory `GalacticArchive`. The wireframe serves as 
a foundation for all Charm Framework applications, empowering you to build incredible 
web applications in the universe.

The setup assistant then guides you through the process.
</div>

## --> Configuration: Fine-Tuning the Hyperdrive

<div class="card card-body" markdown="1">
Now that your project is set up, you can check and adjust the global configuration 
by navigating to the `app/Config` directory. For environment-specific settings, 
explore the `app/Config/Environments/Local` directory.

The active environment is determined by the `app/app.env` file, which contains 
the name of the environment in use. The auto setup process takes care of this for you.
</div>

## --> Web Server Setup: Powering Up the Millennium Falcon

<div class="card card-body" markdown="1">
To get your web server up and running, you might need to adjust its configuration. 
The charm-wireframe comes with a sample `.htaccess` and `nginx.conf` file to help you get started.

For a local development server, simply type `bob serve` in the project directory, and you'll be good to go!
</div>

## --> Manual Installation: The Jedi Path to Charm

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/start/manualinstall.jpg" alt="Manual Installation" /></div>
Welcome back, young Padawan. If you prefer the manual approach to installing the
Charm Framework, fear not, for the Force is strong with you.
Follow these steps to clone the charm-wireframe and prepare your project
for the web development adventure ahead.

### Step 1: Clone the wireframe

First, clone the content of the [neoground/charm-wireframe](https://github.com/neoground/charm-wireframe)
GitHub repository into a new folder on your local machine without initializing it as a new repository:

```bash
git clone --depth 1 https://github.com/neoground/charm-wireframe.git /path/to/new/folder
cd /path/to/new/folder
```

### Step 2: Create Directories for Your Galactic Archive

Next, create the following directories in the root of your project:

```bash
mkdir var/cache var/logs data
```

### Step 3: Set Permissions and Remove Git Data

Set the correct permissions for the newly created directories and remove the charm-wireframe git data:

```bash
chmod -R 0777 var/cache var/logs data
rm -Rf .git
```

### Step 4: Install Dependencies Using Composer

Use Composer to install the required dependencies in your project:

```bash
composer install
```

### Step 5: Create a New Local Environment

Create a new local environment with your custom configuration (e.g. database connection) and set it as default:

```bash
php bob.php c:env Local
```

This will create the file "app/app.env" with the content "Local".

### Step 6: Edit Configuration Files

Edit the "main.yaml" and "connections.yaml" files in the "app/Config/Environments/Local"
directory to match your local development environment:

```bash
vim app/Config/Environments/Local/main.yaml
vim app/Config/Environments/Local/connections.yaml
```

### Step 7: Configure Your Web Server

If you are using Nginx, create a new virtual host configuration for your project
based on the `nginx.conf` example configuration file in the root of the repository.

If you are using Apache, see and adjust the provided `.htaccess` file in the root of the repository.

### Step 8: Launch your project

Finally, open your browser and navigate to your project's URL to see
the Welcome message. You're now ready to start building your own
web applications and APIs using the Charm PHP Framework!

Alternatively, you can use the built-in dev server by executing:

```bash
bob serve
```
</div>

## --> Conclusion

<div class="card card-body" markdown="1">
With this manual installation guide, you've taken a more hands-on approach 
to setting up the Charm PHP Framework. As you embark 
on your web development journey, don't hesitate to consult the documentation 
or reach out to the Charm community for assistance. 
May the Force guide you, young Jedi!
</div>
