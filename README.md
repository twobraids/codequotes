this is an experiment in both git and python

```python
    async def get_enphase_data(self):
        async with aiohttp.ClientSession() as session:
            async with async_timeout.timeout(config.seconds_for_timeout):
                async with session.get(config.target_url) as response:
                    enphase_home_page_raw = await response.text()
        enphase_page = BeautifulSoup(enphase_home_page_raw, 'html.parser')
        # this is stupidly fragile - we're assuming this page format never
        # changes from fetch to fetch - observation has shown this to be ok
        # but don't know if that will hold over Enphase software updates.
        td_elements = enphase_page.find_all('table')[2].find_all('td')
        self.lifetime_generation = self._scale_based_on_units(
            td_elements[self._LIFETIME_GENERATION].contents[0]
        )
        self.generating_now = self._scale_based_on_units(
            td_elements[self._CURRENTLY_GENERATING].contents[0]
        )
        self.microinverter_total = td_elements[self._MICROINVERTER_TOTAL].contents[0]
        self.microinverters_online = td_elements[self._MICROINVERTERS_ONLINE].contents[0]

```
