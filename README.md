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
def draw_a_looping_spiral(a_canvas):
    # the middle of the image
    cartesian_middle_point = CartesianPoint(a_canvas.the_image.size) / 2

    # beginning and end polar points for two loops around a circle
    # while the radius of the loop shrink
    larger_rotator_polar_origin = PolarPoint(
        cartesian_middle_point * (3.0 / 4.0, 0)
    )
    larger_rotator_polar_destination = PolarPoint(0, 4.0 * π)
    larger_rotator_iter = iter_linearly_between(
        larger_rotator_polar_origin, larger_rotator_polar_destination, 2000
    )

    # beginning and end polar points for fifty loops around a circle
    # with the loop radius shrinking with each step
    smaller_rotator_polar_origin = PolarPoint(
        cartesian_middle_point * (1.0 / 8.0, 0)
    )
    smaller_rotator_polar_destination = PolarPoint(0, 100.0 * π)
    smaller_rotator_iter = iter_linearly_between(
        smaller_rotator_polar_origin, smaller_rotator_polar_destination, 2000
    )

    # create a couple iterators that will produce a sequence of polar points
    # that spin in lockstep with each other
    for step_counter, (
        larger_rotated_polar_point,
        smaller_rotated_polar_point,
    ) in enumerate(
        no_consectutive_repeats_iter(
            zip(
                larger_rotator_iter,
                smaller_rotator_iter,
            )
        )
    ):
        # add the cartesian origin CartesianPoint with values from the spinning polar points
        current_cartesion_point = (
            cartesian_middle_point
            + larger_rotated_polar_point
            + smaller_rotated_polar_point
        )
        # draw the line segment from prevous and current cartesian points
        a_canvas.draw_successive_line_segment(current_cartesion_point, step_counter)
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
