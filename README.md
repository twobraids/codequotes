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
square = Path(
    CartesianPoint(0, 0),
    CartesianPoint(0, 10),
    CartesianPoint(10, 10),
    CartesianPoint(10, 0),
)

# translate square by 50 in both x and y directions
translated_square_50 = square + 50

# translate square by 1 in the x direction and 10 in y direction
translated_square_1_10 = square + CartesianPoint(1, 10)

# scale the square by 2 and 3 in the x and y directions respectively
scaled_square_2_3 = square * CartesianPoint(2, 3)

# scale each point of the square by each point of a translated square
scaled_square = square * translated_square_50```

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
