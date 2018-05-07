this is an experiment in both git and python

```python
class ExampleDimmableLight(Thing):
    def __init__(self):
        Thing.__init__('a lamp', 'dimmable light', 'a Web connected lamp')
        self.add_property(
            Property(
                light,
                'level',
                Value(0.0, lambda l: print('New light level is', l)),
                metadata={
                    'type': 'number',
                    'description': 'The level of light from 0-100',
                    'minimum': 0,
                    'maximum': 100,
                }))
```

```python
class ExampleDimmableLight(WoTThing):
    def __init__(self, config, lamp_hardware):
        super(ExampleDimmableLight, self).__init__(
            config, 'a lamp', 'dimmableLight', 'a Web connected lamp')
        
    level = WoTThing.wot_property(
        name='level',
        initial_value=0,
        description="lamp brightness level",
        value_forwarder=_set_hardware_level,
        minimum=0,
        maximum=100
    )
```

```python
class WoTThing(Thing, RequiredConfig):
    @classmethod
    def wot_property(
        kls,
        *,
        name,
        initial_value,
        description,
        value_source_fn=None,
        value_forwarder=None,
        **kwargs
    ):
        kls.wot_property_functions[name] = partial(
            create_wot_property,
            name=name,
            initial_value=initial_value,
            description=description,
            value_source_fn=value_source_fn,
            value_forwarder=value_forwarder,
            **kwargs
        )
```

```python
        if value_source_fn is not None:
            async def a_property_fetching_coroutine(thing_instance):
                while True:
                    try:
                        await value_source_fn(thing_instance)
                    except CancelledError:
                        logging.debug('cancel detected')
                        break
                    except Exception as e:
                        logging.error('loading data fails: %s', e)
                    await sleep(thing_instance.config.seconds_between_polling)

            a_property_fetching_coroutine.property_name = name
            kls.property_fetching_coroutines.append(a_property_fetching_coroutine)
```

```python
            def get_value_fn(thing_instance):
                return thing_instance.properties[name].value.get()
    
            def set_value_fn(thing_instance, new_value):
                thing_instance.properties[name].value.notify_of_external_update(new_value)
    
            return property(get_value_fn, set_value_fn)
```

```python
        current_observation = self.weather_data['current_observation']
        self.temperature = current_observation['temp_f']
        self.barometric_pressure = current_observation['pressure_in']
        self.wind_speed = current_observation['wind_mph']
```

```python
        current_observation = self.weather_data['current_observation']
        self.properties['temperature'].value.notify_of_external_update(
            current_observation['temp_f']
        )
        self.properties['barometric_pressure'].value.notify_of_external_update(
            current_observation['pressure_in']
        )
        self.properties['wind_speed'].value.notify_of_external_update(
            current_observation['wind_mph']
        )
```

```python
    temperature = WoTThing.wot_property(
        name='temperature',
        initial_value=0.0,
        description='the temperature in ℉',
        value_source_fn=get_weather_data,
        units='℉'
    )
    barometric_pressure = WoTThing.wot_property(
        name='barometric_pressure',
        initial_value=30.0,
        description='the air pressure in inches',
        units='in'
    )
    wind_speed = WoTThing.wot_property(
        name='wind_speed',
        initial_value=30.0,
        description='the wind speed in mph',
        units='mph'
    )
```



```python
    async def get_weather_data(self):
        async with aiohttp.ClientSession() as session:
            async with async_timeout.timeout(config.seconds_for_timeout):
                async with session.get(config.target_url) as response:
                    self.weather_data = json.loads(await response.text())
        current_observation = self.weather_data['current_observation']
        self.temperature = current_observation['temp_f']
        self.barometric_pressure = current_observation['pressure_in']
        self.wind_speed = current_observation['wind_mph']
```



