this is an experiment in both git and python

```python

class OneButtonSceneRule(Rule):
    def initial_state(self):
        self.state = 0
        self.old_state = 1
        self.possible_states = [
            (False, False, False, False),
            (True,  True,  True,  True),
            (False, True,  False, True),
            (False, True,  True,  False)
        ]

    def set_state(self, new_state_index):
        self.old_state = self.state
        self.state = new_state_index % len(self.possible_states)
        new_state = self.possible_states[self.state]
        self.hue_1.on = new_state[0]
        self.hue_2.on = new_state[1]
        self.hue_3.on = new_state[2]
        self.hue_4.on = new_state[3]

    def register_triggers(self):
        self.command_button.subscribe_to_event('pressed')
        self.command_button.subscribe_to_event('doublePressed')
        self.command_button.subscribe_to_event('longPressed')
        return (self.command_button, )
    
    def action(self, the_triggering_thing, the_trigger_event, new_value):
        if the_trigger_event == "pressed":
            self.set_state(self.state + 1)
        elif the_trigger_event == "doublePressed":
            if self.state != 0:
                self.set_state(0)
            else:
                self.set_state(self.old_state)
        elif the_trigger_event == "longPressed":
            self.set_state(0)

```
