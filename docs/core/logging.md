---
key:     core.logging
title:   Logging
section: Core Modules
nav:
  prev:
    page: core.http
    icon: prev
    name: HTTP
  next:
    page: core.mailman
    icon: next
    name: Mailman
---

# ->>  Logging <<-

<div class="card card-body" markdown="1">
Embark on a digital trail with the Logging module, your trusted companion in capturing 
the whispers of code, be it a gentle information or a critical outcry. Access this 
singleton harbinger of messages via `C::Logging()->...`, and unveil the tales of your
application's odyssey.
</div>

## ->> Methods and Examples

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/printer.jpg" alt="Printer" /></div>

This class extends the Psr LoggingInterface, so you can use this class like any other standard logger:

| Method    | Syntax                                                         | Description / Use Case                               | 
|-----------|----------------------------------------------------------------|------------------------------------------------------|
| withName  | `withName(string $name): Logging`                              | Add a log entry with a custom name.                  |
| debug     | `debug(Stringable $message, array $context = []): void`        | Detailed debug information.                          |
| emergency | `emergency(Stringable $message, array $context = []): void`    | System is unusable.                                  |
| alert     | `alert(Stringable $message, array $context = []): void`        | Action must be taken immediately.                    |
| critical  | `critical(Stringable $message, array $context = []): void`     | Critical conditions.                                 |
| error     | `error(Stringable $message, array $context = []): void`        | Runtime errors that do not require immediate action. |
| warning   | `warning(Stringable $message, array $context = []): void`      | Exceptional occurrences that are not errors.         |
| notice    | `notice(Stringable $message, array $context = []): void`       | Normal but significant events.                       |
| info      | `info(Stringable $message, array $context = []): void`         | Interesting events.                                  |
| log       | `log($level, Stringable $message, array $context = []): void`  | Logs with an arbitrary level.                        |

### -> Examples

```php
// Adding a log entry with a custom name:
C::Logging()->withName('foobar')->alert('Test Message');

// Detailed debug information:
C::Logging()->debug('Debug message', $contextArray);

// System is unusable:
C::Logging()->emergency('System failure');

// And so forth for other log levels...
```

### -> Events

If you want to implement an action if a specific log level entry is logged, you can simply add an EventListener.

At each logging an event is fired in module `Logging`, name is the log level, for example `emergency`.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

Harness the eloquence of the Logging module to chronicle the voyage of your application 
through the code cosmos. Tailor the log entries with custom names, or categorize them 
with varied levels of urgency. The debug bar, when enabled, becomes a window to the log
entries, enriching your debugging endeavors. Venture forth, with the Logging module guarding 
the annals of your code journey.

</div>
