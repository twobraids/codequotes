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

from configman import ArgumentParser

parser = ArgumentParser(description='Process some integers.')
parser.add_argument('integers', metavar='N', type=int, nargs='+',
                     help='an integer for the accumulator')
parser.add_argument('--sum', dest='accumulate', action='store_const',
                    const=sum, default=max,
                    help='sum the integers (default: find the max)')

args = parser.parse_args()
print(args.accumulate(args.integers))

```

```python

    import numpy.fft
    from itertools import permutations 

```

```python
    import sister_module_1
    from sister_module_2 import some_obscure_symbol    

```

```bash

$ ./x1.py 0 0 --help
    usage: x1.py [-h] [--sum] [--admin.print_conf ADMIN.PRINT_CONF]
                 [--admin.dump_conf ADMIN.DUMP_CONF] [--admin.strict]
                 [--admin.conf ADMIN.CONF]
                 N [N ...]

    Process some integers.

    positional arguments:
      N                     an integer for the accumulator

    optional arguments:
      -h, --help            show this help message and exit
      --sum                 sum the integers (default: find the max)
      --admin.print_conf ADMIN.PRINT_CONF
                            write current config to stdout (json, py, ini, conf)
      --admin.dump_conf ADMIN.DUMP_CONF
                            a file system pathname for new config file (types:
                            json, py, ini, conf)
      --admin.strict        mismatched options generate exceptions rather than
                            just warnings
      --admin.conf ADMIN.CONF
                            the pathname of the config file (path/filename)


```
