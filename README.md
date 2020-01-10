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

    from __future__ import absolute_import

```

```python

    import numpy.fft
    from itertools import permutations 

```

```python
    import sister_module_1
    from sister_module_2 import some_obscure_symbol    

```

```python

    from . import sister_module_1
    from .sister_module_2 import some_obscure_symbol
    from .. import aunt_module_3 
    from ..uncle_package_4 import cousin_module_5

```
