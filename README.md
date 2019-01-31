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
    offset: "-01:00:00"  
  action:
    service: light.turn_on

```

```python
class EveningPorchLightRule(Rule):
    def register_triggers(self):
        self.sunset_trigger = SunsetTrigger(
            lat_long=(44.562951, -123.3535762),
            elevation=70.0,
            time_offset="1h"
        )
        return self.sunset_trigger

    def action(self, *args):
        self.porch_light.on = True

```
