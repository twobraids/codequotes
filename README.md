this is an experiment in both git and python

```python
class MorningWakeRule(Rule):

    def register_triggers(self):
        morning_wake_trigger = AbsoluteTimeTrigger("morning_wake_trigger", "06:30:00")
        return (morning_wake_trigger,)

    def action(self, *args):
        self.Bedside_Ikea_Light.on = True
        
    
    
class AbsoluteTimeTrigger(TimeBasedTrigger):
    def __init__(
        self,
        name,
        # time_of_day_str should be in the 24Hr form "HH:MM:SS"
        time_of_day_str,
    ):
        super(AbsoluteTimeTrigger, self).__init__(name)
        self.trigger_time = datetime.strptime(time_of_day_str, '%H:%M:%S').time()

    async def trigger_detection_loop(self):
        logging.debug('Starting timer %s', self.trigger_time)
        while True:
            time_until_trigger_in_seconds = self.time_difference_in_seconds(
                self.trigger_time,
                datetime.now().time()
            )
            logging.debug('timer triggers in %sS', time_until_trigger_in_seconds)
            await asyncio.sleep(time_until_trigger_in_seconds)
            self._apply_rules('activated', True)
            await asyncio.sleep(1)



class MorningWakeRule(Rule):

    @property
    def today_is_a_weekday(self):
        weekday = datetime.now().date().weekday()  # M0 T1 W2 T3 F4 S5 S6
        return weekday in range(5)

    @property
    def today_is_a_weekend_day(self):
        return not self.today_is_a_weekday

    def register_triggers(self):
        self.weekday_morning_wake_trigger = AbsoluteTimeTrigger(
            "morning_wake_trigger", "06:30:00"
        )
        self.weekend_morning_wake_trigger = AbsoluteTimeTrigger(
            "morning_wake_trigger", "07:30:00"
        )
        return (self.weekday_morning_wake_trigger, self.weekend_morning_wake_trigger)

    def action(self, the_changed_thing, *args):
        if the_changed_thing is self.weekday_morning_wake_trigger:
            if self.today_is_a_weekday:
                self.Bedside_Ikea_Light.on = True
        elif the_changed_thing is self.weekend_morning_wake_trigger:
            if self.today_is_a_weekend_day:
                self.Bedside_Ikea_Light.on = True



class MorningWakeRule(Rule):

    @property
    def today_is_a_weekday(self):
        weekday = datetime.now().date().weekday()  # M0 T1 W2 T3 F4 S5 S6
        return weekday in range(5)

    @property
    def today_is_a_weekend_day(self):
        return not self.today_is_a_weekday

    def register_triggers(self):
        self.weekday_morning_wake_trigger = AbsoluteTimeTrigger(
            "weekday_morning_wake_trigger", "06:10:00"
        )
        self.weekend_morning_wake_trigger = AbsoluteTimeTrigger(
            "weekend_morning_wake_trigger", "07:10:00"
        )
        return (self.weekday_morning_wake_trigger, self.weekend_morning_wake_trigger)

    def action(self, the_changed_thing, *args):
        if the_changed_thing is self.weekday_morning_wake_trigger:
            if self.today_is_a_weekday:
                asyncio.ensure_future(self._off_to_full())
        elif the_changed_thing is self.weekend_morning_wake_trigger:
            if self.today_is_a_weekend_day:
                asyncio.ensure_future(self._off_to_full())

    async def _off_to_full(self, ):
        for i in range(20):
            new_level = (i + 1) * 5
            self.Bedside_Ikea_Light.on = True
            self.Bedside_Ikea_Light.level = new_level
            await asyncio.sleep(60)


```
