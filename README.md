this is an experiment in both git and python

```python

class DailySolarEventsTrigger(TimeBasedTrigger):
    def __init__(
        self,
        config,
        name,
        # list of any daily events (see self.all_possible_event_names)
        event_name_list,
        lat_long_tuple,
        timezone_name,  # like "US/Pacific" or "UTC"
        elevation_in_meters,
        # modify the event time - should be a signed integer in string form with an
        # optional H, h, M, m, S, s, D, d  as a suffix to indicate units
        # default is S
        offset='0s'
    ):
        super(DailySolarEventsTrigger, self).__init__(config, name)
        self.event_name_list = event_name_list
        self.location = astral.Location((
            "location_name",
            "location_region",
            lat_long_tuple[0],
            lat_long_tuple[1],
            timezone_name,
            elevation_in_meters
        ))
        self.offset = timedelta(0, self.duration_str_to_seconds(offset))
        self.one_day = timedelta(1)
        self.all_possible_event_names = (
            "blue_hour_start",
            "blue_hour_end",
            "dawn",
            "daylight_start",
            "daylight_end",
            "dusk",
            "golden_hour_start",
            "golden_hour_end",
            "night_start",
            "night_end",
            "rahukaalam_start",
            "rahukaalam_end",
            "solar_midnight",
            "solar_noon",
            "sunrise",
            "sunset",
            "twilight_start",
            "twilight_end",
        )

    def get_schedule(self):
        event_list = []
        for an_event_name in self.event_name_list:
            if an_event_name not in self.all_possible_event_names:
                error_message = "{}  is not a valid event name".format(an_event_name)
                logging.error(error_message)
                continue

            base_event_name = an_event_name.replace('_end', '').replace('_start', '')
            try:
                event = getattr(self.location, base_event_name)()
            except Exception as e:
                # astral will raise exceptions if any of the sun events
                # cannot be calculated - for example there is no sunrise
                # or sunset in mid summer of mid winter.
                logging.error(e)
                continue

            if isinstance(event, datetime):
                event_list.append((event + self.offset, an_event_name))
                continue

            if isinstance(event, tuple):
                # the tuples are all (start_datetime, end_datetime) except for
                # the 'night' event where they are returned as (end_datetime, start_datetime)
                index = 0 if an_event_name.endswith('_start') else 1
                if base_event_name == 'night':
                    event = (event[1], event[0])
                event_list.append((event[index] + self.offset, an_event_name))
                continue
        return event_list

    async def trigger_event(self, now, time_delta, event_name):
        logging.info('%s in %s seconds (%s)', event_name, time_delta.total_seconds(), now + time_delta)
        await asyncio.sleep(time_delta.total_seconds())
        self._apply_rules(event_name)

    async def trigger_detection_loop(self):
        while True:
            event_schedule = self.get_schedule()
            for event_datetime, event_name in event_schedule:
                logging.debug('new schedule %s %s', event_name, event_datetime)
                now = self.now_in_timezone(self.location.tz)
                if event_datetime < now:
                    continue
                time_delta = event_datetime - now
                asyncio.ensure_future(self.trigger_event(now, time_delta, event_name))

            now = self.now_in_timezone(self.location.tz)
            next_day = (now + self.one_day).date()

            next_schedule_time = self.local_timezone.localize(datetime(  # next day at 1am
                next_day.year,
                next_day.month,
                next_day.day,
                1
            ))
            time_interval_until_next_schedule = next_schedule_time - now
            logging.info(
                "%s: next day's schedule pulled in %s seconds (%s))",
                self.name,
                time_interval_until_next_schedule.total_seconds(),
                next_schedule_time
            )

            await asyncio.sleep(time_interval_until_next_schedule.total_seconds())


class EveningPorchLightRule(Rule):

    def register_triggers(self):
        self.sunset_trigger = DailySolarEventsTrigger(
            self.config,
            "sunset_trigger",
            ("sunset", ),
            (44.562951, -123.3535762),
            "US/Pacific",
            70.0,
            "10m"  # ten minutes
        )
        self.ten_pm_trigger = AbsoluteTimeTrigger(
            self.config,
            'ten_pm_trigger',
            '22:00:00'
        )
        return (self.sunset_trigger, self.ten_pm_trigger)

    def action(self, the_triggering_thing, *args):
        if the_triggering_thing is self.sunset_trigger:
            self.Philips_HUE_01.on = True
        else:
            self.Philips_HUE_01.on = False


class RahukaalamRule(Rule):

    def register_triggers(self):
        rahukaalam_trigger = DailySolarEventsTrigger(
            self.config,
            "rahukaalam_trigger",
            ("rahukaalam_start", "rahukaalam_end", ),
            (44.562951, -123.3535762),
            "US/Pacific",
            70.0,
        )
        return (rahukaalam_trigger,)

    def action(self, the_triggering_thing, the_trigger, *args):
        if the_trigger == "rahukaalam_start":
            logging.info('%s starts', self.name)
            self.Philips_HUE_02.on = True
            self.Philips_HUE_02.color = "#FF9900"
        else:
            logging.info('%s ends', self.name)
            self.Philips_HUE_02.on = False



```
