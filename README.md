# GPS Jamming Demo

Uses latest Earthscope SDK to retrieve observation and ephemeris data to detect GPS jamming using the C/No method.

<figure>
  <img src="./images/0225_GPS_March_interference.jpg" alt="2019 military GPS jamming map">
  <figcaption>Areas where the military is conducting GPS interference on March 1. Image generated with TARGETS courtesy of MITRE.</figcaption>
</figure>

## TBD

- I don't think nest_asyncio is necessary. I believe Jupyter supports await in cells for several years now. Might depend on the kernel.
- The obs table can come back with 4charid if you prefer instead of 9charid. You can use the gnss_observations(..., meta_fields=[...]) arg to control which columns return. Might simplify your join logic and avoid the discussion of 9char vs 4char
- Good catch on mismatch between un/signed sat uint8 vs int8. That should be consistent u8 - sat ids are not negative. We can fix that upstream and simplify this notebook
- The A session should be 15s, not 30s.
- You request sat pos with an elevation filter of 0° then later filter to 10°. Just seems like redundant work. Using the latter would drop lower elevations in the initial join without needing subsequent .filter(...)