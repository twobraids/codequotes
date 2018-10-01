this is an experiment in both git and python

```python
class BondedBulbsRule(Rule):

    def register_triggers(self):
        return (
            self.Philips_HUE_01,
            self.Philips_HUE_02,
            self.Philips_HUE_03,
            self.Philips_HUE_04,
        )

    def action(self, the_triggering_thing, the_changed_property_name, the_new_value):
        for a_thing in self.participating_things.values():
            setattr(a_thing, the_changed_property_name, the_new_value)
```
