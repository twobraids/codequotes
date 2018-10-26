this is an experiment in both git and python

```python

class IncrementalTimerRule(Rule):

    def register_triggers(self):
        self.delay_timer = DelayTimer(self.config, "adjustable_delay", "10m")
        self.Button2.subscribe_to_event('pressed')
        self.Button2.subscribe_to_event('longPressed')
        return (self.Button2, self.delay_timer, self.Philips_HUE_03)

    def action(self, the_triggering_thing, the_trigger_event, new_value):
        logging.debug('action %s %s %s', the_triggering_thing.name, the_trigger_event, new_value)

        if the_triggering_thing is self.Button2 and the_trigger_event == 'pressed':
            if self.Philips_HUE_03.on:
                logging.info('%s adding %s', self.name, self.delay_timer.original_timer_period_str)
                self.delay_timer.add_time()  # add ten minutes
            else:
                self.Philips_HUE_03.on = True

        elif the_triggering_thing is self.Button2 and the_trigger_event == 'longPressed':
            self.delay_timer.cancel()
            self.Philips_HUE_03.on = False

        elif the_triggering_thing is self.delay_timer:
            self.Philips_HUE_03.on = False

        elif the_triggering_thing is self.Philips_HUE_03 and new_value is False:
            self.delay_timer.cancel()

        elif the_triggering_thing is self.Philips_HUE_03 and new_value is True:
            logging.info('%s adding %s', self.name, self.delay_timer.original_timer_period_str)
            self.delay_timer.add_time()  # add ten minutes

        else:
            logging.debug('action ignored')





```
