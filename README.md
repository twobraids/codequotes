this is an experiment in both git and python

```python
class ExampleIfRule(Rule):

    def register_triggers(self):
        return (self.Philips_HUE_01,)

    def action(self, *args):
        if self.Philips_HUE_01.on:
            self.Philips_HUE_02.on = True
            self.Philips_HUE_03.on = True
            self.Philips_HUE_04.on = True


class ExampleWhileRule(Rule):

    def register_triggers(self):
        return (self.Philips_HUE_01,)

    def action(self, the_triggering_thing, the_changed_property_name, the_new_value):
        if the_changed_property_name == 'on':
            self.Philips_HUE_02.on = the_new_value
            self.Philips_HUE_03.on = the_new_value
            self.Philips_HUE_04.on = the_new_value

```
