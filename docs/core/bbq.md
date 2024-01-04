---
key:     core.bbq
title:   Queue (BBQ)
section: Core Modules
nav:
  prev:
    page: core.mailman
    icon: prev
    name: Mailman
  next:
    page: core.request
    icon: next
    name: Request
---

# ->> BarBeQueue (BBQ) - Our Queue System <<-

<div class="card card-body" markdown="1">
BarBeQueue (BBQ), our adept queue system, orchestrates the orderly processing of tasks, adhering to the time-honored FIFO (First In, First Out) principle, yet with a dash of priority-based discernment, ensuring a meticulous execution of queued entries.

- **Queue Mechanism**: Typical to any queue system, entries are added and await their turn for processing.
- **Priority Ordering**: Entries bear a priority tag (1 to 5), determining their place in the queue, 1 being the highest priority.
- **Multiple Queues**: Spawn multiple queues each with a distinct name, catering to different task domains.

</div>

## ->> Running Queue Jobs

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/queue.jpg" alt="Section header image" /></div>

Queue jobs are invoked via a CLI command, circumventing the internal cron to bolster performance and handling. Tailor the queue run frequency to your needs, though a 1 to 5-minute interval is often judicious.

```cronexp
*/5 * * * * /usr/bin/php /path/to/app/bob.php queue:run --name=default >> /dev/null 2>&1
```

This crontab entry nudges the `default` queue into action every 5 minutes.

You can also have multiple calls to work queues in parallel.
An instance runs as long as there are jobs in its queue, then terminates.

</div>

## ->> Creating Queue Jobs

<div class="card card-body" markdown="1">

Crafting a queue entry is a straightforward endeavor. Instantiate a `QueueEntry`, designate the 
method to execute, and thrust it into the queue. You can call this anywhere in your code.

```php
use Charm\Barbequeue\QueueEntry;
use Charm\Vivid\C;

$entry = new QueueEntry();
$entry->setMethod('App\Controllers\MyClass::sendEmail')
    ->setPriority(3);
C::Queue()->push($entry);
```

For a more nuanced interaction, pass an array of arguments to the method:

```php
$entry = new QueueEntry();
$entry->setMethod('App\Controllers\MyClass::sendEmail', [$user->email, $user->name])
    ->setPriority(3);
C::Queue()->push($entry);
```

Thus, `App\Controllers\MyClass::sendEmail($user->email, $user->name)` is invoked when the queue processes this entry.

Please note that the called method must be `public static`.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

BBQ is not just a queue system, but a beacon of order amidst the asynchronous chaos, 
a conductor orchestrating the symphony of tasks with a calm, priority-tempered baton.

</div>
