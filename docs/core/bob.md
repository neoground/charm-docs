---
key:     core.bob
title:   Bob Command Line Interface
section: Core Modules
nav:
  prev:
    page: core.arrays
    icon: prev
    name: Arrays
  next:
    page: core.cache
    icon: next
    name: Cache
---

# ->> Bob - Our Command-Line Interface <<-

<div class="card card-body" markdown="1">
In the vast expanses of your digital realm, the command-line interface (CLI) beckons as a potent ally. Bob, 
our CLI module, is your gateway to harnessing the power of Charm through the alacritous environment
of the console. Sculpted atop the venerable Symfony/Console package, Bob opens the portals to 
creating and executing CLI commands with an elegance reminiscent of the masterful orchestration 
witnessed in the symphonies of the stars.

In a galaxy not so far away, Bob (short for Binary Operations Butler) was created to serve as the 
ultimate command-line companion for Charm Framework developers. It's so easy to use, even a Wookiee could do it!

Before delving into Bob's domain, a brief sojourn into the philosophy of 
[Symfony/Console](https://symfony.com/doc/current/components/console.html) is warranted. 
At its core, Symfony/Console is designed to ease the creation and management of command-line interfaces.
With a penchant for modularity and extendability, it empowers developers to craft commands, define 
input arguments, and orchestrate the rendering of output - a symphony of functionality played in harmony.
</div>

## ->> Engaging with Bob

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/bob-mod.jpg" alt="Section header image" /></div>

At the heart of your app's base directory, the invocation `php bob.php` unveils the ensemble of available commands, 
each a note in your development melody. For those with the
[Charm-Toolkit](https://github.com/neoground/charm-toolkit) at their disposal
(highly recommended when you have CLI access), 
Bob transcends to a global command, simplifying the invocation to a mere `bob`.

Just try it out in your charm app - and explore the built-in commands and help:

```bash
php bob.php
```

</div>

## ->> Create CLI Commands

<div class="card card-body" markdown="1">

The creation of new console commands is a breeze with Bob.
Utilizing the blueprint provided, the command `php bob.php c:cc` sets the stage,
guiding you through the process with the grace of a maestro.

In the serene alleys of `app/Jobs/Console`, commands find their abode. Here, the `DemoCommand` class, 
akin to a virtuoso, demonstrates the art of crafting a console command. The `configure` method sets the stage,
naming the command and painting a description. As the curtain rises with the `execute` method, 
the logic orchestrates its performance, rendering its melody to the console, 
culminating in a triumphant 'It is working. Yay!'

```php
namespace App\Jobs\Console;

use Symfony\Component\Console\Command\Command;
use Symfony\Component\Console\Input\InputInterface;
use Symfony\Component\Console\Output\OutputInterface;

class DemoCommand extends Command
{

    /**
     * The configuration
     */
    protected function configure()
    {
        $this->setName("demo:mycommand")
            ->setDescription("A simple demo command");
    }

    protected function execute(InputInterface $input, OutputInterface $output)
    {
        // Your logic goes here

        $output->writeln('It is working. Yay!');
        return self::SUCCESS;
    }
}
```

Simply call your script via `php bob.php demo:mycommand`.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

Bob, your CLI maestro, not only bridges the realms of web and console but empowers you to conduct your 
development symphony with a finesse that echoes through the realms of efficiency and elegance.
Whether crafting new commands or invoking the built-in magics, Bob ensures your journey through
the CLI realm is nothing short of legendary.

</div>
