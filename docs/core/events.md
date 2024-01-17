---
key:     core.events
title:   Events
section: Core Modules
nav:
  prev:
    page: core.database
    icon: prev
    name: Database
  next:
    page: core.formatter
    icon: next
    name: Formatter
---

# ->>  Events <<-

<div class="card card-body" markdown="1">
Within the vast expanse of the Charm framework, the Event module emerges as a beacon of synchrony, 
orchestrating a ballet of interactions between different realms of your application. 
It empowers developers with the ability to weave a rich tapestry of reactive programming, 
where disparate parts of the codebase can converse in a harmonized choreography. 
Just as the celestial bodies in a far-off galaxy communicate through the ethereal whispers 
of the cosmos, the components of your application engage in a dialogue through the medium 
of events, orchestrated by this adept conductor.

These events are very similar to JavaScript events. You can create EventListener and you can fire your own Events.

</div>

## ->> Core Methods & Events

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/event1.jpg" alt="Section title image" /></div>

The Event module brandishes two potent methods in its armory:

### -> Retrieving Listeners of an Event

`getListeners($module, $name): false|null|array`

Delves into the ether to unveil the listeners that lie in wait for a particular event's call. For instance, to inquire about the listeners of a "DemoEvent" within the "App" module, you would invoke:
```php
C::Event()->getListeners('App', 'DemoEvent');
```

### -> Firing an Event

`fire($module, $name): bool`

Sends forth the call of an event into the cosmos of your application, beckoning the awaiting listeners to spring into action. For example, to herald the occurrence of a "DemoEvent" within the "App" module, you would invoke:
```php
C::Event()->fire('App', 'DemoEvent');
```

### -> Available built-in Events

| Module     | Event         | Fired when...                                        | Description                                                                           |
|------------|---------------|------------------------------------------------------|---------------------------------------------------------------------------------------|
| `Charm`    | `shutdown`    | The application is shutting down                     | This is the last event you can use. After this the system terminates.                 |
| `View`     | `renderStart` | The render method of a twig view is executed         | Use this to inject data to a view right before it is rendered.                        |
| `Redirect` | `renderStart` | The render method of a redirect response is executed |                                                                                       |
| `Json`     | `renderStart` | The render method of a json response is executed     |                                                                                       |
| `File`     | `renderStart` | The render method of a file response is executed     |                                                                                       |
| `Queue`    | `push`        | An entry is added to a queue                         |                                                                                       |
| `Queue`    | `run`         | The queue starts running                             |                                                                                       |
| `Queue`    | `done`        | The queue has finished                               |                                                                                       |
| `Crown`    | `run`         | Crown is running                                     | This is probably fired every minute - every time crown runs.                          |
| `Logging`  | `loglevel`    | A log entry is added                                 | Available log levels: debug, emergency, alert, critical, error, warning, notice, info |

</div>

## ->> Creating and Listening to Custom Events

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/event2.jpg" alt="Section title image" /></div>

Creating your event is akin to crafting a star, a beacon in the code space. To birth a new event, employ your module name and a unique event name, like so:
```php
C::Event()->fire('MyModuleName', 'sampleEvent');
```

And as celestial bodies heed the call of a new star, so do event listeners respond to
the birth of your event. Create your own guardian of events by crafting 
an event listener within the `app/System/EventListener` domain.

Utilize this exemplar, or summon a blueprint via CLI using `bob c:ev`. This guardian,
the `RenderEvent` class, will heed the call of the `sampleEvent` event
from `MyModuleName`, ready to spring into action when the event fires:

```php
namespace App\System\EventListener;

use Charm\Events\EventListener;
use Charm\Vivid\C;

class RenderEvent extends EventListener
{
    protected function configure()
    {
        $this->fireOnEvent("MyModuleName", "sampleEvent");
    }

    public function fire()
    {
        // Engage in your celestial dance here.
    }
}
```

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

The Event module stands as a stellar navigator, guiding the flow of communication 
within your application's cosmos. It's not merely a module, but a maestro, 
orchestrating a symphony of reactive interactions that breathe life into the 
cold void of code logic. As you traverse further into the heart of Charm, let 
the Event module be your compass, your beacon amidst the swirling nebula of code, 
leading you towards crafting applications that are not just responsive, but alive to the rhythm of events.

</div>
