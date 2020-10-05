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
config = config_manager.get_config()
print config.arg1, config.arg2, config.arg3

n.add_option(
    name='filename',
    doc='the name of the file',
    default=None,
    is_argument=True
)
n.add_option(
    name='action',
    doc='the action to take on the file',
    default='echo',
)    

config = config_manager.get_config()
with open(config.filename) as fp:
    do_something_interesting(fp)




def echo(x):
    print x

def backwards(x):
    print x[::-1]

def upper(x):
    print x.upper()

n = Namespace()
n.add_option(
    'action',
    default=None,
    doc='the action to take [echo, backwards, upper]',
    short_form='a',
    is_argument=True,
    from_string_converter=class_converter
)
n.add_option(
    'text',
    default='Socorro Forever',
    doc='the text input value',
    short_form='t',
    is_argument=True,
)
c = ConfigurationManager(
    n,
    app_name='demo1',
    app_description=__doc__
)
try:
    config = c.get_config()
    config.action(config.text)
except AttributeError, x:
    print "%s is not a valid command"
except TypeError:
    print "you must specify an action"
```

```python
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
