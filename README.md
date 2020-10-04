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
class MessageHandlerBase(object):

    def send_message(self, *args, **kwargs):
        raise NotImplemented

    def broadcast_message(self, *args, **kwargs):
        raise NotImplemented

class A(object):
    """talk to someone"""

    def send_message(self, message):
        person = self.find_someone()
        person.talk_to_me(message_broken)

    def broadcast_message(self, message):
        self.shout(message)
            

class B(object):
    """send message via radio broadcast""" 

    def broadcast_message(self, message):
        self.radio.broadcast(message)


class C(MessageHandlerBase):
    """send message by waving flags"""

        def broadcast_message(self, message):
        self.flags.wave_message(message)


def notify_of_emergency(a_message_handler):
    """Notify a specific person of an emergency condition.  If that is
    not possible, broadcast the emergency message"""
    message = "the sky is falling!"
    try:
        # try to send the message
        a_message_handler.send_message(message)
    except NotImplemented:
        # fallback to broadcasting the message
        a_message_handler.broadcast_message(message)            
```

```python
    import sister_module_1
    from sister_module_2 import some_obscure_symbol    

```

```bash

$ ./x1.py --admin.dump_conf=x1.ini
$ cat x1.ini
# sum the integers (default: find the max)
#accumulate=max
# an integer for the accumulator
#integers=


$ ./x1.py 1 2 3
6
$ ./x1.py 4 5 6
15


$ cat x1.ini
# sum the integers (default: find the max)
#accumulate=max
# an integer for the accumulator
integers=1 2 3 4 5 6
$ ./x1.py
6
$ ./x1.py --sum
21


$ export accumulate=sum
$ ./x1.py 1 2 3
6
$ ./x1.py 1 2 3 4 5 6
21





```
