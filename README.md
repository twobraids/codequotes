this is an experiment in both git and python

```python
async with aiohttp.ClientSession() as session:
    async with async_timeout.timeout(config.seconds_for_timeout):
        async with session.put(
            "http://gateway.local/things/{}/properties/color".format(config.thing_id),
            headers={
                'Accept': 'application/json',
                'Authorization': 'Bearer {}'.format(config.thing_gateway_auth_key),
                'Content-Type': 'application/json'
            },
            data='{{"color": "{}"}}'.format(a_color)
        ) as response:
            return await response.text()

```
