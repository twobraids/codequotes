this is an experiment in both git and python

```python

url = 'http://gateway.local/things'
headers = {
    'Accept': 'application/json',
    'Authorization': 'Bearer {}'.format(auth),
}

async def get_all_things(self):
    async with aiohttp.ClientSession() as session:
        async with session.get(url, headers=headers) as resp:
            all_things_meta = json.loads(await resp.text())
```
