this is an experiment in both git and python

```python

class TimeOutLightRule(Rule):

    def register_triggers(self):
        self.timer = DelayTimer(self.config, "time_out time", "5s")
        self.command_button.subscribe_to_event('pressed')
        self.command_button.subscribe_to_event('longPressed')
        self.command_button.subscribe_to_event('doublePressed')
        return (self.command_button, self.timer, self.hue_4)

    def action(self, the_triggering_thing, the_trigger_event, new_value):
        if the_triggering_thing is self.command_button and the_trigger_event == 'pressed':
            if self.hue_4.on:
                self.timer.add_time()  # add five seconds
            else:
                self.hue_4.on = True

        elif the_triggering_thing is self.command_button and the_trigger_event == 'longPressed':
            self.hue_4.on = False

        elif the_triggering_thing is self.command_button and the_trigger_event == 'doublePressed':
            self.hue_4.on = not self.hue_4.on

        elif the_triggering_thing is self.timer:
            self.hue_4.on = False

        elif the_triggering_thing is self.hue_4 and new_value is False:
            self.timer.cancel()

        elif the_triggering_thing is self.hue_4 and new_value is True:
            self.timer.add_time()  # add five seconds


```
