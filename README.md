this is an experiment in both git and python

```python

class RedLightRule(Rule):
    def register_triggers(self):
        self.command_button.subscribe_to_event('pressed')
        return (self.command_button, )

    def action(self, *args):
            self.hue_3.on = not self.hue_3.on
```
