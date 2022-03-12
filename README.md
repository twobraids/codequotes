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

```pythondef draw_path_demo(a_canvas):
    """Draw 9 looping rays from the center of the canvas"""

    canvas_middle_point = CartesianPoint(a_canvas.the_image.size) / 2

    collection_of_ray_paths = []

    for θ in iter_linear_steps_between(0, 2 * π, 9):

        # materialize a path of PolarPoints making a straight ray from the origin
        ray_path = Path(
            iter_linear_steps_between(PolarPoint(0, θ), PolarPoint(300, θ), 100)
        )

        # materialize a spiral path of PolarPoints about the origin
        spiral_path = Path(
            iter_natural_steps_between(PolarPoint(0, 0), PolarPoint(50, 10 * π), 100)
        )

        # combine the straight rays with the spiral path and translate them
        # from the canvas origin to the canvas middle - save the result as
        # a path of PolarPoints
        collection_of_ray_paths.append(ray_path + spiral_path + canvas_middle_point)

    # set up windowing iterators for all the spiraling ray paths
    windowed_iter_for_every_ray_path = (
        windowed(a_ray_path, 2) for a_ray_path in collection_of_ray_paths
    )

    # step through the all the spiral ray paths in parallel, round robin style
    for a_segment_for_every_ray in zip(*windowed_iter_for_every_ray_path):
        for start_point, end_point in a_segment_for_every_ray:
            a_canvas.draw_line_segment(start_point, end_point)


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
