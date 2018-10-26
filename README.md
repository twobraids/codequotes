this is an experiment in both git and python

```python

class PantryLightTimerRule(Rule):

    def register_triggers(self):
        self.delay_timer = DelayTimer(self.config, "adjustable_delay", "10m")
        self.PantryButton.subscribe_to_event('pressed')
        self.PantryButton.subscribe_to_event('longPressed')
        return (self.PantryButton, self.delay_timer, self.PantryLight)

    def action(self, the_triggering_thing, the_trigger_event, new_value):
        logging.debug('action %s %s %s', the_triggering_thing.name, the_trigger_event, new_value)

        if the_triggering_thing is self.PantryButton and the_trigger_event == 'pressed':
            if self.PantryLight.on:
                logging.info('%s adding %s', self.name, self.delay_timer.original_timer_period_str)
                self.delay_timer.add_time()  # add ten minutes
            else:
                self.PantryLight.on = True

        elif the_triggering_thing is self.PantryButton and the_trigger_event == 'longPressed':
            self.delay_timer.cancel()
            self.PantryLight.on = False

        elif the_triggering_thing is self.delay_timer:
            self.PantryLight.on = False

        elif the_triggering_thing is self.PantryLight and new_value is False:
            self.delay_timer.cancel()

        elif the_triggering_thing is self.PantryLight and new_value is True:
            logging.info('%s adding %s', self.name, self.delay_timer.original_timer_period_str)
            self.delay_timer.add_time()  # add ten minutes

        else:
            logging.debug('action ignored')






```
