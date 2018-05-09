this is an experiment in both git and python

```python
    lifetime_generation = WoTThing.wot_property(
        name='lifetime_generation',
        initial_value=0.0,
        description='Total lifetime generation in KWh',
        value_source_fn=get_enphase_data,
        units='KWh'
    )
    generating_now = WoTThing.wot_property(
        name='generating_now',
        initial_value=0.0,
        description='currently generating in KWh',
        units='KW'
    )
    microinverter_total = WoTThing.wot_property(
        name='microinverter_total',
        initial_value=0,
        description='the number of microinverters installed'
    )
    microinverters_online = WoTThing.wot_property(
        name='microinverters_online',
        initial_value=0,
        description='the number of micro inverters online',
    )
```
