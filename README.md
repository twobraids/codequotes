I like the way that github highlights python code. In my own blogs and presentations,
I want to highlight code in the same manner. Each commit in this repo represents a single
code quote. This repo gives both a linkable history and a source for mining HTML for code
quotes inserted into wikis, blogs and presentations. I like the consistency and flexibility
of github's CSS tagging in code quotes.


```yaml
automation:
  alias: Turn on the porch light an hour after the sun sets
  initial_state: true
  hide_entity: false
  trigger:
    platform: sun
    event: sunset
    offset: "01:00:00"  
  action:
    service: porchlight.turn_on

```

```python
class WeatherStation(WoTThing):
    def __init__(self, config):
        super(WeatherStation, self).__init__(...)
        
    async def get_weather_data(self): ...
        
    temperature = WoTThing.wot_property(
        name='temperature',
        initial_value=0.0,
        description='the temperature in ℉',
        value_source_fn=get_weather_data,
        units='℉'
    )


async def get_weather_data(self):
    async with aiohttp.ClientSession() as session:
        async with session.get(self.config.target_url) as response:
            weather_data = json.loads(await response.text())
    self.temperature = weather_data['current_observation']['temp_f']
                
```
