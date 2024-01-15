---
key:     core.crown
title:   Schedule (Crown)
section: Core Modules
nav:
  prev:
    page: core.request
    icon: prev
    name: Request
  next:
    page: core.server-session
    icon: next
    name: Server & Session
---

# ->> Crown: The Automated Timekeeper <<-

<div class="card card-body" markdown="1">
In the vast realm of programming, time is a dimension where scheduled tasks reign. Crown, your loyal timekeeper, orchestrates these automated rituals, ensuring the consistent heartbeat of your application's chronology.
</div>

## ->> Installation

<div class="card card-body" markdown="1">
Embark on the journey by invoking the CLI Command `bob cron:run` 
every minute via your system's cron job or systemd timer. 
Here's a sample incantation for a cron job:

```cron
* * * * * /usr/bin/php /path/to/basedir/bob.php cron:run >> /dev/null 2>&1
```
</div>

## ->> Crafting a Cron Job

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/clock1.jpg" alt="Section header image" /></div>

Forge your cron jobs in the sacred halls of `app/System/Jobs/Cron`. 
Use the mystical blueprint command `bob c:cj` or derive your creation from this ancient scripture:

```php
namespace App\Jobs\Cron;

use Charm\Crown\Cronjob;

class Demo extends Cronjob
{
    protected function configure(): void
    {
        $this->setName('Demo command')
            ->runWeekly();
    }

    public function run(): int
    {
        // This will be executed every time this job runs.
        return self::SUCCESS;
    }
}
```

</div>

## ->> The Sands of Time

<div class="card card-body" markdown="1">
<div class="mb-4"><img src="*ASSETS*/charm/core/clock2.jpg" alt="Section header image" /></div>

In the realm of `Crown`, time bends to your will, allowing you to schedule the invocation of your 
tasks with precision. Utilize the following incantations within the `configure()` method of your 
Cronjob class to set the rhythm of your tasks:

| Method                                                                       | Description                                          |
|------------------------------------------------------------------------------|------------------------------------------------------|
| `runDaily($hour = 0, $min = 0)`                                              | Daily invocation at the specified hour and minute    |
| `runHourly($min = 0)`                                                        | Hourly chant at the specified minute                 |
| `runEveryHalfHour($offset = 0)`                                              | Chime every half hour with an optional offset        |
| `runEveryQuarterHour($offset = 0)`                                           | Quarter-hourly toll with an optional offset          |
| `runWeekly($day = 1, $hour = 0, $min = 0)`                                   | Weekly summon on a specified day, hour, and minute   |
| `runEveryMonday($hour = 0, $min = 0)`                                        | Weekly on Monday at specified hour and minute        |
| `runEveryTuesday($hour = 0, $min = 0)`                                       | Weekly on Tuesday at specified hour and minute       |
| `runEveryWednesday($hour = 0, $min = 0)`                                     | Weekly on Wednesday at specified hour and minute     |
| `runEveryThursday($hour = 0, $min = 0)`                                      | Weekly on Thursday at specified hour and minute      |
| `runEveryFriday($hour = 0, $min = 0)`                                        | Weekly on Friday at specified hour and minute        |
| `runEverySaturday($hour = 0, $min = 0)`                                      | Weekly on Saturday at specified hour and minute      |
| `runEverySunday($hour = 0, $min = 0)`                                        | Weekly on Sunday at specified hour and minute        |
| `runMonthly($day = 1, $hour = 0, $min = 0)`                                  | Monthly on a specified day, hour, and minute         |
| `runQuarterly($day = 1, $hour = 0, $min = 0)`                                | Quarterly on a specified day, hour, and minute       |
| `runYearly($month = 1, $day = 1, $hour = 0, $min = 0)`                       | Yearly on a specified month, day, hour, and minute   |
| `setSchedule($min = '*', $hour = '*', $dom = '*', $month = '*', $dow = '*')` | Craft your own temporal spell with a custom schedule |

Each method beckons the `Crown` to awaken your tasks at the destined time, engraving your intentions onto the fabric of the cosmos.

Keep in mind that the Crown system uses cron notation as well. So you can set ranges and values just like
in your crontab.

</div>

## ->> Conclusion

<div class="card card-body" markdown="1">

With Crown, you've not just a tool, but a loyal timekeeper, ensuring that your tasks are summoned 
in precise accordance with the cosmic clock, letting you focus on conquering other realms 
in the vast universe of development.

</div>
