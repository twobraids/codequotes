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
class Vector(tuple):
    def __new__(cls, *args):
        match (args):
            case [cls() as an_instance_of_cls]:
                # match instances of the calling cls or its derivatives
                # this is the identity case
                return an_instance_of_cls

            case [Vector() as an_instance_of_vector]:
                # match any instance of the Vector family not directly in line with cls
                # explicitly invoke a conversion - maybe cartesian to polar or vice versa
                return cls.as_my_type(an_instance_of_vector)

            case [Iterable() as an_iterable]:
                # match any old iterable like a generator or numpy array
                # create a new instance of this cls
                return super().__new__(
                    cls,
                    tuple(cls._judge_candidate_value(n) for n in an_iterable),
                )

            case args_:
                # discrete values were passed, assume they are to be the coordinate
                # values of a new instance of this cls
                return super().__new__(
                    cls, tuple(cls._judge_candidate_value(n) for n in args_)
                )

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
