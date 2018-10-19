this is an experiment in both git and python

```python

class RainbowRule(Rule):

    def initial_state(self):
        self.participating_bulbs = (
            self.Philips_HUE_01,
            self.Philips_HUE_02,
            self.Philips_HUE_03,
            self.Philips_HUE_04,
            self.Philips_HUE_05,
            self.Philips_HUE_06,
        )

        for a_bulb, initial_color in zip(self.participating_bulbs, the_rainbow_of_colors):
            a_bulb.on = True
            a_bulb.color = initial_color

    def register_triggers(self):
        self.heartbeat = HeartBeat(self.config, 'the heart', "2s")
        return (self.heartbeat, )

    def action(self, *args):
        the_rainbow_of_colors.rotate(1)
        for a_bulb, new_color in zip(self.participating_bulbs, the_rainbow_of_colors):
            a_bulb.color = new_color

```
