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
    @classmethod
    def as_my_type(cls, the_other):
        # This function is in charge of converting things into polar coordinates.
        # The base class Vector has no sense of what its members mean, so members of the
        # polar branch of the Vector family interpret base Vector instances and other
        # Iterables as having polar values already.
        match the_other:
            case PolarPoint():
                # identity case
                return the_other

            case Point() as a_cartesian_point:
                # we know this is the cartesian case, so we must explicitly convert it
                return cls.as_polar(a_cartesian_point)

            case Iterable() as an_iterator:
                # we don't know what this sequence represents.
                # To be consistent with the constructor, assume they are
                # series of components of a polar point
                return cls(*an_iterator)

            case Number() as ρ:
                # a rare case where a PolarPoint is specified with ρ alone and
                # θ, φ are assumed to be zero.
                return cls(ρ)

            case _:
                raise TypeError(f"Don't know how to convert {the_other} to Polar")
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
