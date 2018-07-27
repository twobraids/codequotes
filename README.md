this is an experiment in both git and python

```python
async def monitor_and_propagate_state(config, thing_id):
    global suppress_state_change
    suppress_state_change_max = len(config.list_of_thing_ids) - 1
    while True:
        # loop forever to re-establish the web socket if it fails for some reason
        try:
            async with websockets.connect(
                'ws://gateway.local/things/{}?jwt={}'.format(
                    thing_id,
                    config.things_gateway_auth_key
                ),
            ) as websocket:
                async for a_message_txt in websocket:
                    a_message = json.loads(a_message_txt)
                    if a_message['messageType'] == 'propertyStatus':
                        if suppress_state_change:
                            logging.debug('%s suppress action', thing_id)
                            suppress_state_change -= 1
                            continue
                        for a_property in a_message["data"].keys():
                            a_value = a_message["data"][a_property]
                            logging.debug("propagate send %s %s", a_property, a_value)
                            suppress_state_change = suppress_state_change_max
                            change_property_for_all_things(config, thing_id, a_property, a_value)
        except websockets.exceptions.ConnectionClosed:
            # the connection has unexpectedly closed.
            # re-establish it by continuing the loop
continue
```
