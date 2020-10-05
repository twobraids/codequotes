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
top_level = cm.Namespace()
top_level.source = cm.Namespace(doc="the input source")
top.level.source.option(
    "storageClass",
    doc="the classname for the source",
    default="socorro.storage.crashstorage.DatabaseCrashStorage",
    from_string_converer=cm.class_converter,
)
top_level.destination = cm.Namespace(doc="the output destination")
top_level.destination.option(
    "storageClass",
    doc="the classname for the destination",
    default="socorro.storage.crashstorage.HBaseCrashStorage",
    from_string_converter=cm.class_converter,
)


print config.source.hostname
print config.source.port
print config.destination.hostname
print config.destination.port

source.storageClass = socorro.storage.crashstorage.HBaseCrashStorage
source.hostname = hbase1
destination.storageClass = socorro.storage.crashstorage.HBaseCrashStorage
destination.hostname = hbase2
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
