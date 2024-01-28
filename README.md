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


def distance(p1, p2):
    return sqrt((p2.x - p1.x) ** 2 + (p2.y - p1.y) ** 2)


str_to_Point = partial(
    str_to_list, item_converter=float, list_to_collection_converter=Point
)


def all_points_within_block_iter(a_block):
    for x in range(a_block.left, a_block.right):
        for y in range(a_block.upper, a_block.lower):
            yield Point(x, y)


required_config = Namespace()
required_config.add_option(
    "A", default=Point(58.34, 844.29), 
    doc="point A", 
    from_string_converter=str_to_Point
)

required_config.add_option(
    "B",
    default=Point(846.05, 290.27),
    doc="point B",
    from_string_converter=str_to_Point,
)
required_config.add_option(
    "C",
    default=Point(1574.73, 453.96),
    doc="point C",
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


config = configuration(required_config)

A_in_px = config.A
B_in_px = config.B
C_in_px = config.C
scale = config.AB_in_m / distance(A_in_px, B_in_px)
search_box_in_px = Block(400, 1000, 1200, 2000)


def test_fitness(test_point_in_px):
    SA_in_m = distance(A_in_px, test_point_in_px) * scale
    SB_in_m = distance(B_in_px, test_point_in_px) * scale
    SC_in_m = distance(C_in_px, test_point_in_px) * scale

    TA_in_s = SA_in_m / config.speed_of_sound_in_mps
    TB_in_s = SB_in_m / config.speed_of_sound_in_mps
    TC_in_s = SC_in_m / config.speed_of_sound_in_mps

    diff_AB = abs(TB_in_s - TA_in_s)
    if not isclose(diff_AB, 4.02, abs_tol=0.1):
        return 10000

    diff_AC = abs(TA_in_s - TC_in_s)
    if not isclose(diff_AC, 5.72, abs_tol=0.1):
        return 10000

    diff_BC = abs(TB_in_s - TC_in_s)
    if not isclose(diff_BC, 1.7, abs_tol=0.1):
        return 10000

    # return the deviation from the sum of the deltas as a fittness value
    return abs(diff_AB + diff_AC + diff_BC - 4.02 - 5.72 - 1.7)


best_fitness = 1000000
best_point = None
for test_point_in_px in all_points_within_block_iter(search_box_in_px):
    fitness = test_fitness(test_point_in_px)
    if fitness < best_fitness:
        best_fitness = fitness
        best_point = test_point_in_px


print(f'{best_point=} at {best_fitness=}')


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
