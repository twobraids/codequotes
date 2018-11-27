this is an experiment in both git and python

```python

class ThingTalker:
    def __init__(self, config):
        self.command_queue = asyncio.Queue()
        self.connect_str = '{}?jwt={}'.format(
            web_socket_link_str,
            auth_key
        )

    async def trigger_detection_loop(self):
        while True:
            async with websockets.connect(self.connect_str) as websocket:
                await asyncio.gather(
                    self.receive_websocket_messages(websocket),
                    self.send_queued_messages(websocket)
                )

    async def receive_websocket_messages(self, websocket):
        async for raw_message in websocket:
            message = json.loads(raw_message)
            self.act_on_message(message)

    async def send_queued_messages(self, websocket):
        while True:
            message = await self.command_queue.get()
            message_str = json.dumps(message)
            await websocket.send(message_str)
```
