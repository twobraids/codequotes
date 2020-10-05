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
app_definition = cm.Namespace()
app_definition.option(
    "_application",
    doc="the fully qualified class of the application",
    default=some_default_class,
    from_string_converter=cm.class_converter,
)

config_manager = cm.ConfigurationManager((app_definition,), (ConfigParser, os.environ, getopt))
config = config_manager.get_config()

application_class = config._application
app_instance = application_class(config)
logger.info("starting %s", application_class.app_name)
app_instance.main()


import os.path
import socarro.configman as cm
import socorro.database as sdb
import socorro.lib.gzip_csv as gzcsv


class DailyCsvApp(object):

    app_name = "daily_csv"
    app_version = "1.1"
    app_doc = "This app produces a csv file of the current day's crash data"

    required_config = cm.Namespace()
    required_config.option(
        name="day",
        doc="the date to dump (YYYY-MM-DD)",
        default=dt.date.today().isoformat(),
        from_string_converter=cm.date_converter,
    )
    required_config.option(
        name="outputPath", doc="the path of the gzipped csv output file", default="."
    )
    required_config.option("product", doc="the name of the product to dump", default="Firefox")
    required_config.option(name="version", doc="the name of the version to dump", default="4.%")
    # get database connection option definitions from the database module
    required_config.update(sdb.get_required_config())

    def __init__(self, config):
        self.config = config

    def main(self):
        with config.database.transaction() as db_conn:
            output_filename = ".".join(
                self.config.product, self.config.version, self.config.day.isoformat()
            )
            csv_pathname = os.path.join(self.config.outputPath, output_filename)
            db_query = self.construct_query(
                self.config.day, self.config.product, self.confg.version
            )
            with gzcsv(csv_pathname) as csv_fp:
                for a_row in sdb.query(db_conn, db_query):
                    csv_fp.write_row(a_row)

    def construct_query(self, day, product, version):
        # implementation omitted for brevity
        pass```

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
