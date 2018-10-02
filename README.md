this is an experiment in both git and python

```python
class HeartBeat(TimeBasedTrigger):
    def __init__(
        self,
        name,
        period_str
        # duration should be a integer in string form with an optional
        #    H, h, M, m, S, s, D, d  as a suffix to indicate units - default S
    ):
        super(HeartBeat, self).__init__(name)
        self.period = self.duration_str_to_seconds(period_str)

    async def trigger_dection_loop(self):
        logging.debug('Starting heartbeat timer %s', self.period)
        while True:
            await asyncio.sleep(self.period)
            logging.info('%s beats', self.name)
            self._apply_rules()

```
