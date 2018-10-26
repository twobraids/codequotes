this is an experiment in both git and python

```python

class CombinationLightRule(Rule):

    def initial_state(self):
        self.index = 0
        self.combinations = [
            (False, False, False),
            (True, False, False),
            (True, True, False),
            (True, True, True),
            (False, True, True),
            (False, False, True),
            (False, True, False),
            (True, False, True),
        ]

    def register_triggers(self):
        self.KitchenButton.subscribe_to_event('pressed')
        self.KitchenButton.subscribe_to_event('longPressed')
        return (self.KitchenButton, )

    def set_bulb_state(self):
        self.StoveLight.on = self.combinations[self.index][0]
        self.CounterLight.on = self.combinations[self.index][1]
        self.SinkLight.on = self.combinations[self.index][2]

    def action(self, the_triggering_thing, the_trigger_event, new_value):
        if the_trigger_event == "pressed":
            self.index = (self.index + 1) % len(self.combinations)
            self.set_bulb_state()

        elif the_trigger_event == "longPressed":
            self.index = 0
            self.set_bulb_state()






```
