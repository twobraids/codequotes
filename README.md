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
class CartesianPoint(Vector):
    @staticmethod
    def _judge_candidate_value(a_potential_scalar):
        # accept only scalars as values
        if isinstance(a_potential_scalar, Number):
            return a_potential_scalar
        raise TypeError(f"members must be scalar, {a_potential_scalar} is not")

    def as_cartesian(self, cartesian_point_class=None):
        # Since the base coordinate type in this system is cartesian, there is
        # very little to be done here: this instance is already known to be cartesian.
        # The existance of this method is to be symetric with the PolarPoint branch
        # of the Vector family
        if cartesian_point_class is None:
            # identity case - since we know that self is already cartesian
            return self
        # not a very useful thing here, but the equivalent method in the PolarPoint
        # class allows conversion to any specified cartesian_point_class
        return cartesian_point_class(*self)

    @classmethod
    def as_my_type(cls, the_other):
        # This function is in charge of converting things into cartesian coordinates.
        # The base class Vector has no sense of what its members mean, so members of the
        # cartesian branch of the Vector family interpret base Vector instances and other
        # Iterables as having cartesian values already.
        match (the_other):
            case cls():
                # Match an instance of this cls or its derivatives - identity case
                #   For example cls may be CartesianPoint but IntPoints would match
                #   because an IntPoint is a CartesianPoint
                return the_other

            case Vector():
                # match an instance of base class Vector, but of another lineage
                # other than CartesianPoint.  For example, this ensures that a
                # PolarPoint is properly converted to Cartesian.
                try:
                    return the_other.as_cartesian(cls)
                except AttributeError:
                    # Vector itself doesn't know anything about being cartesian, so just
                    # make a new instance of cls from it
                    return cls(*the_other)

            case Iterable():
                # make an instance of cls from any iterable assuming that the
                # coordinate values are already cartesian.
                return cls(*the_other)

            case _:
                raise TypeError(
                    f"No conversion defined for {the_other.__class__} to {cls}"
                )

    @property
    def x(self):
        try:
            return self[0]
        except IndexError:
            return 0

    @property
    def y(self):
        try:
            return self[1]
        except IndexError:
            return 0

    @property
    def z(self):
        try:
            return self[2]
        except IndexError:
            return 0


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
