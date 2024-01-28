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
#!/usr/bin/env python3

from math import sqrt, isclose
from functools import partial

from points import Point, Block
from configmanners import Namespace, configuration
from configmanners.converters import str_to_list

terrible_number = 100000

def distance(p1, p2):
    return sqrt((p2.x - p1.x) ** 2 + (p2.y - p1.y) ** 2)


str_to_Point = partial(
    str_to_list, item_converter=float, list_to_collection_converter=Point
)

str_to_Block = partial(
    str_to_list, item_converter=int, list_to_collection_converter=Block
)


def all_points_within_block_iter(a_block):
    for x in range(a_block.left, a_block.right):
        for y in range(a_block.upper, a_block.lower):
            yield Point(x, y)


required_config = Namespace()
required_config.add_option(
    "A_in_px",
    default=Point(58.34, 844.29),
    doc="point A in pixel coordinates",
    from_string_converter=str_to_Point,
)

required_config.add_option(
    "B_in_px",
    default=Point(846.05, 290.27),
    doc="point B in pixel coordinates",
    from_string_converter=str_to_Point,
)
required_config.add_option(
    "C_in_px",
    default=Point(1574.73, 453.96),
    doc="point C in pixel coordinates",
    from_string_converter=str_to_Point,
)
required_config.add_option(
    "AB_time_delta",
    default=4.0,
    doc="time delta between listening posts A and B",
    from_string_converter=str_to_Point,
)
required_config.add_option(
    "AC_time_delta",
    default=6.0,
    doc="time delta between listening posts A and C",
    from_string_converter=str_to_Point,
)
required_config.add_option(
    "BC_time_delta",
    default=2.0,
    doc="time delta between listening posts B and C",
    from_string_converter=str_to_Point,
)
required_config.add_option(
    "AB_in_m",
    default=3800.0,
    doc="distance in meters between points A and B",
)
required_config.add_option(
    "speed_of_sound_in_mps",
    default=332.24,
    doc="the speed of sound in meters per second",
)
required_config.add_option(
    "search_box_in_px",
    default="400, 1000, 1200, 2000",
    doc="coodinate extents in pixels of the search area",
    from_string_converter=str_to_Block,
)


config = configuration(required_config)

scale = config.AB_in_m / distance(config.A_in_px, config.B_in_px)


def test_fitness(test_point_in_px):
    SA_in_m = distance(config.A_in_px, test_point_in_px) * scale
    SB_in_m = distance(config.B_in_px, test_point_in_px) * scale
    SC_in_m = distance(config.C_in_px, test_point_in_px) * scale

    TA_in_s = SA_in_m / config.speed_of_sound_in_mps
    TB_in_s = SB_in_m / config.speed_of_sound_in_mps
    TC_in_s = SC_in_m / config.speed_of_sound_in_mps

    test_AB_delta = abs(TB_in_s - TA_in_s)
    if not isclose(test_AB_delta, config.AB_time_delta, abs_tol=0.1):
        return terrible_number

    test_AC_delta = abs(TA_in_s - TC_in_s)
    if not isclose(test_AC_delta, config.AC_time_delta, abs_tol=0.1):
        return terrible_number

    test_BC_delta = abs(TB_in_s - TC_in_s)
    if not isclose(test_BC_delta, config.BC_time_delta, abs_tol=0.1):
        return terrible_number

    # return the deviation from the sum of the deltas as a fittness value
    return abs(
        test_AB_delta
        + test_AC_delta
        + test_BC_delta
        - config.AB_time_delta
        - config.AC_time_delta
        - config.BC_time_delta
    )


best_fitness = terrible_number
best_point = None
for test_point_in_px in all_points_within_block_iter(config.search_box_in_px):
    fitness = test_fitness(test_point_in_px)
    if fitness < best_fitness:
        best_fitness = fitness
        best_point = test_point_in_px


if best_point is not None:
    print(f'{best_point=} at {best_fitness=}')
else:
    print('the air cannon is not in the search area')
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
