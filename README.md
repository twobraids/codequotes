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
class Path(Vector):
    @classmethod
    def _judge_candidate_value(cls, a_potential_point):
        # accept only scalars as values
        if isinstance(a_potential_point, Vector):
            return a_potential_point
        raise TypeError(
            f'{cls} members must be a Vector instance, "{a_potential_point}" is not'
        )

    def _operation(self, the_other, a_dyadic_fn):
        # return a new instance with members that result from a_dyadic_fn applied to
        # this instance zipped with the_other
        match the_other:
            case Number() as a_number:
                # match scalars
                return self.__class__(
                    *starmap(
                        a_dyadic_fn, zip_longest(self, (a_number,), fillvalue=a_number)
                    )
                )

            case self.__class__() as a_path_object:
                return self.__class__(*starmap(a_dyadic_fn, zip(self, a_path_object)))

            case CartesianPoint() | PolarPoint():
                # match any instance of the two point families
                return self.__class__(
                    *starmap(
                        a_dyadic_fn,
                        zip_longest(self, (the_other,), fillvalue=the_other),
                    )
                )

            case Iterable() as an_iterable:
                # match any other type of iterable
                return self.__class__(*starmap(a_dyadic_fn, zip(self, an_iterable)))

            case _:
                # no idea how to apply this value in a dyadic manner with this Vector instance
                raise TypeError(f"{the_other} disallowed")

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
