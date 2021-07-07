I like the way that github highlights python code. In my own blogs and presentations,
I want to highlight code in the same manner. Each commit in this repo represents a single
code quote. This repo gives both a linkable history and a source for mining HTML for code
quotes inserted into wikis, blogs and presentations. I like the consistency and flexibility
of github's CSS tagging in code quotes.


```yaml
automation:
  alias: Turn on the porch light an hour after the sun sets
  initial_state: true
  hide_entity: false
  trigger:
    platform: sun
    event: sunset
    offset: "01:00:00"  
  action:
    service: porchlight.turn_on

```

```python
class RuleTrigger:
    __match_args__ = ('name',)

    def __init__(self, config, name):
        self.config = config
        self.name = name
        self.rules_that_use_this_thing = []
        self.canceled = False


class OzoneRule(Rule):

    def register_triggers(self):
        self.heartbeat = HeartBeat(self.config, 'the_heart', "20s")
        self.ozone_on_timer = DelayTimer(self.config, "ozone_on_timer", "5s")
        self.total_cycle_timer = DelayTimer(self.config, "total_cycle_timer", "2m")
        self.total_cycle_timer.add_time()
        self.end_of_cycle_timer = DelayTimer(self.config, "end_of_cycle_timer", "10s")
        return (self.heartbeat, self.ozone_on_timer, self.total_cycle_timer, self.end_of_cycle_timer)

    def action(self, the_trigger, the_event, new_value):
        logging.info('OzoneRule action %s %s %s', the_trigger.name, the_event, new_value)

        match(the_trigger):
            case HeartBeat('the_heart') if self.total_cycle_timer.is_running:
                print(f'{datetime.now()} heartbeat - ozone on')
                self.ozone_switch.on = True
                self.ozone_on_timer.add_time()
            case DelayTimer('ozone_on_timer'):
                print(f'{datetime.now()} ozone_timer - ozone off')
                self.ozone_switch.on = False
            case DelayTimer('total_cycle_timer'):
                self.ozone_on_timer.cancel()
                print(f'{datetime.now()} total_cycle_timer - ozone off')
                self.ozone_switch.on = False
                self.end_of_cycle_timer.add_time()
            case DelayTimer('end_of_cycle_timer'):
                print(f'{datetime.now()} end_of_cycle_timer - shutdown')
                exit(-1)

```

```python
```

```bash

$ ./x1.py --admin.dump_conf=x1.ini
$ cat x1.ini
# sum the integers (default: find the max)
#accumulate=max
# an integer for the accumulator
#integers=


$ ./x1.py 1 2 3
6
$ ./x1.py 4 5 6
15


$ cat x1.ini
# sum the integers (default: find the max)
#accumulate=max
# an integer for the accumulator
integers=1 2 3 4 5 6
$ ./x1.py
6
$ ./x1.py --sum
21


$ export accumulate=sum
$ ./x1.py 1 2 3
6
$ ./x1.py 1 2 3 4 5 6
21





```
