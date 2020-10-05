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
import config_manager as cm

n = cm.Namespace()
n.option(
    "storageClass",
    doc="a class name for storage",
    default="socorro.storage.crashstorage.HBaseCrashStorage",
    from_string_converter=cm.class_converter,
)
conf_man = cm.ConfigurationManager([n], application_name="sample")
config = conf_man.get_config()
print config.storageClass


rc = cm.Namespace()
rc.option(
    name="hbaseHost",
    doc="Hostname for HBase/Hadoop cluster. May be a VIP or load balancer",
    default="localhost",
)
rc.option(name="hbasePort", doc="HBase port number", default=9090)
rc.option(name="hbaseTimeout", doc="timeout in milliseconds for an HBase connection", default=5000)
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
