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
def __init__(self, config, quit_check_callback=None):
    super(ElasticSearchCrashStorage, self).__init__(config, quit_check_callback)
    self.transaction = config.transaction_executor_class(config, self, quit_check_callback)
    if self.config.elasticsearch_urls:
        self.es = pyelasticsearch.ElasticSearch(self.config.elasticsearch_urls, timeout=self.config.timeout)
        settings_json = open(self.config.elasticsearch_index_settings).read()
        self.index_settings = json.loads(settings_json % self.config.elasticsearch_doctype)
    else:
        config.logger.warning('elasticsearch crash storage is disabled.')
```

```python

    import numpy.fft
    from itertools import permutations 

```

```python
    import sister_module_1
    from sister_module_2 import some_obscure_symbol    

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
