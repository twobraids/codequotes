this is an experiment in both git and python

```python

the_rainbow_of_colors = deque([
    '#ff0000',
    '#ffaa00',
    '#aaff00',
    '#00ff00',
    '#0000ff',
    '#aa00ff'
])


class RainbowRule(Rule):

    def initial_state(self):
        self.participating_bulbs = (
            self.hue_1,
            self.hue_2,
            self.hue_3,
            self.hue_4,
            self.hue_5,
            self.hue_6,
        )

        for a_bulb, initial_color in zip(self.participating_bulbs, the_rainbow_of_colors):
            with a_bulb.batch_communication() as bulb_transaction:
                bulb_transaction.on = True
                bulb_transaction.color = initial_color

    def register_triggers(self):
        self.heartbeat = HeartBeat(self.config, 'the heart', "2s")
        return (self.heartbeat, )

    def action(self, *args):
        the_rainbow_of_colors.rotate(1)
        for a_bulb, new_color in zip(self.participating_bulbs, the_rainbow_of_colors):
            a_bulb.color = new_color


```
