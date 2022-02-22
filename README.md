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
    def _operation(self, the_other, a_dyadic_fn):
        # return a new instance with members that result from a_dyadic_fn applied to
        # this instance zipped with the_other
        match (the_other):
            case Number() as a_number:
                # match scalars
                return self.__class__(
                    *starmap(
                        a_dyadic_fn, zip_longest(self, (a_number,), fillvalue=a_number)
                    )
                )

            case Vector() as a_vector:
                # match any instance of the Vector family
                the_other_as_my_type = self.as_my_type(a_vector)
                return self.__class__(
                    *starmap(a_dyadic_fn, zip(self, the_other_as_my_type))
                )

            case Iterable() as an_iterable:
                # match any other type of iterable
                return self.__class__(*starmap(a_dyadic_fn, zip(self, an_iterable)))

            case _:
                # no idea how to apply this value in a dyadic manner with this Vector instance
                raise TypeError(f"{the_other} disallowed")

    def __add__(self, the_other):
        return self._operation(the_other, add)

    def __sub__(self, the_other):
        return self._operation(the_other, sub)

    def __mul__(self, the_other):
        return self._operation(the_other, mul)

    def __floordiv__(self, the_other):
        return self._operation(the_other, floordiv)

    def __truediv__(self, the_other):
        return self._operation(the_other, truediv)

    def __pow__(self, the_other):
        return self._operation(the_other, pow)

    def __neg__(self):
        return self.__class__(*(-c for c in self))

    def trunc(self):
        return self.__class__(*(int(c) for c in self))

    def round(self):
        return self.__class__(*(round(c) for c in self))

    def dot(self, the_other):
        return sum(a * b for a, b in zip(self, the_other))

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
