this is an experiment in both git and python

```python

class BlueLightRule(Rule):
    def register_triggers(self):
        self.command_button.subscribe_to_event('pressed')
        return (self.command_button, )

    def action(self, *args):
        with self.hue_3.batch_communication() as hue_3:
            hue_3.on = not self.hue_3.on
            if hue_3.on is True:
                hue_3.color = "#0000ff"
```
