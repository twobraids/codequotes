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
def iter_linear_steps_between(
    start, stop, number_of_iterations, target_type=lambda n: n
):
    # in cartesian space, make a sequence of points representing
    # a straight line between the start and stop points
    increment = (stop - start) / number_of_iterations
    for i in range(number_of_iterations):
        yield target_type(start + (increment * i))


def iter_natural_steps_between(
    start, stop, number_of_iterations, target_type=lambda n: n
):
    # In cartesian space, Vectors and CartesianPoints trace out straight
    # lines between the start and end points. PolarPoints trace curves
    # based on the full magnitude of the angular components (number of time
    # around the circle). I use this iterator for making spiral paths.
    base_point_type = start.__class__
    for p in zip(
        *(
            iter_linear_steps_between(first, second, number_of_iterations)
            for first, second in zip(start, stop)
        )
    ):
        yield target_type(base_point_type(*p))

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
