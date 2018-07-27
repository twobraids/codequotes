this is an experiment in both git and python

```python
    async with websockets.connect(
        'ws://gateway.local/things/{}?jwt={}'.format(
            thing_id,
            config.things_gateway_auth_key
        ),
    ) as websocket:
        async for a_message_txt in websocket:
            a_message = json.loads(a_message_txt)
            if a_message['messageType'] == 'propertyStatus':
                for a_property in a_message["data"].keys():
                    a_value = a_message["data"][a_property]
                    suppress_state_change = suppress_state_change_max
                    change_property_for_all_things(config, thing_id, a_property, a_value)

    global suppress_state_change
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
                    suppress_state_change -= 1
                    continue
                for a_property in a_message["data"].keys():
                    a_value = a_message["data"][a_property]
                    suppress_state_change = suppress_state_change_max
                    change_property_for_all_things(config, thing_id, a_property, a_value)





```
