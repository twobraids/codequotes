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
class Alpha(object):
    """This is a silly class that does very very little"""
    def __init__(self, config):
        self.config = config

    def do_something(self, data):
        if isinstance(data, basestring):
            return ''.join(x for x in 'you think this is silly?'
                                if x not in 'aoeui')
        elif isinstance(data, Number):
            return 2 * data
        else:
            return data

    def do_something_else(self, data):
        if data is None:
            return True
        else:
            raise TypeError('only None is acceptable')


from numbers import Number

#==============================================================================
class Alpha(object):
    """This is a silly class that does very very little"""
    #--------------------------------------------------------------------------
    def __init__(self, config):
        self.config = config
    #--------------------------------------------------------------------------
    def do_something(self, data):
        if isinstance(data, basestring):
            return ''.join(x for x in 'you think this is silly?'
                                if x not in 'aoeui')
        elif isinstance(data, Number):
            return 2 * data
        else:
            return data
    #--------------------------------------------------------------------------
    def do_something_else(self, data):
        if data is None:
            return True
        else:
            raise TypeError('only None is acceptable')

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
