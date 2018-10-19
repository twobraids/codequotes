this is an experiment in both git and python

```python

class SunTrigger(TimeBasedTrigger):
    def __init__(
        self,
        config,
        name,
        sun_event_name,  # dawn, sunrise, noon, sunset, dusk
        lat_long_tuple,
        timezone_name,  # like "US/Pacific" or "UTC"
        elevation_in_meters,
        time_offset_in_seconds=0
    ):
        super(SunTrigger, self).__init__(config, name)
        self.sun_event_name = sun_event_name
        self.location = astral.Location((
            "location_name",
            "location_region",
            lat_long_tuple[0],
            lat_long_tuple[1],
            timezone_name,
            elevation_in_meters
        ))
        self.time_offset = timedelta(0, time_offset_in_seconds)
        self.one_day = timedelta(1)

    def get_sun_schedule(self, now):
        try:
            return self.location.sun(now)
        except Exception:
            # astral will raise exceptions if any of the sun events
            # cannot be calculated - for example there is no sunrise
            # in midwinter or sunset in mid summer in some locations.
            # Guess by returning now + one day
            return {self.sun_event_name: now + self.one_day}

    async def trigger_detection_loop(self):
        while True:
            now = self.local_now().astimezone(self.location.tz)
            sun_schedule = self.get_sun_schedule(now)
            if sun_schedule[self.sun_event_name] + self.time_offset < now:
                # this event is in the past, get tomorrow's event instead
                sun_schedule = self.get_sun_schedule(now + self.one_day)

            time_until_trigger_in_seconds = self.time_difference_in_seconds(
                sun_schedule[self.sun_event_name] + self.time_offset,
                now
            )
            logging.debug('timer triggers in %sS', time_until_trigger_in_seconds)
            await asyncio.sleep(time_until_trigger_in_seconds)
            self._apply_rules('activated', True)
            await asyncio.sleep(1)
            
  class EveningPorchLightRule(Rule):

    def register_triggers(self):
        sun_trigger = SunTrigger(
            self.config,
            "sun_trigger",
            "sunset",
            (44.562951, -123.3535762),
            "US/Pacific",
            70.0,
            600  # ten minutes
        )
        return (sun_trigger,)

    def action(self, *args):
        self.FrontPorchLight.on = True

def main(config, rule_system):
    my_rule = EveningPorchLightRule(
        config,
        rule_system,
        'turn on front porch light ten minutes after sunset'
    )
    rule_system.add_rule(my_rule)

            
```
