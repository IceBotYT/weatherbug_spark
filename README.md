# WeatherBug Spark

A library for interacting with the [WeatherBug Spark](https://www.weatherbug.com/alerts/spark/) service to get the lightning strike locations and closest lightning strike distance.

WeatherBug Spark is a service that can detect both cloud-to-ground and in-cloud lightning made possible by the WeatherBug's proprietary Total Lightning Network™.

## Installation

Linux:
```bash
python3 -m pip install weatherbug-spark
```

Windows:
```
py -m pip install weatherbug-spark
```

## Usage

```python
import asyncio
import weatherbug_spark

async def main():
    data = await weatherbug_spark.get_data(latitude=42.3601, longitude=-71.0589)

    # Get the closest strike distance
    print(data.closestPulseDistance) # float

    # Get the local lightning strike locations
    print(data.pulseListAlert) # List of LightningStrike objects

    # Get the global lightning strike locations
    print(data.pulseListGlobal) # List of LightningStrike objects

    # Get the short message
    print(data.shortMessage) # Monitor Storms

    # Get the long message
    print(data.safetyMessage) # You are not in immediate danger now, but stay alert and frequently check WeatherBug ...

    # Get the hex code for the color of the alert
    print(data.alertColor) # #F0D701

if __name__ == "__main__":
    asyncio.run(main())
```

## Classes
`get_data` returns a `SparkResult` object, with included `LightningStrike` objects.

### `SparkResult`

| Field                 | Type                  | Description                                                    |
| --------------------- | --------------------- | -------------------------------------------------------------- |
| alertCode             | int                   | The alert code. The higher the number, the closer the strikes. |
| alertColor            | str                   | The hex code for the color of the alert.                       |
| closestPulseDistance  | float                 | The closest lightning strike distance in miles.                |
| closestPulseDirection | float                 | The closest lightning strike direction in degrees.             |
| pulseListAlert        | list[LightningStrike] | The local lightning strike locations.                          |
| pulseListGlobal       | list[LightningStrike] | The global lightning strike locations.                         |
| shortMessage          | str                   | The short message.                                             |
| safetyMessage         | str                   | The long message.                                              |

### `LightningStrike`

| Field            | Type  | Description                                                          |
| ---------------- | ----- | -------------------------------------------------------------------- |
| latitude         | float | The latitude of the lightning strike.                                |
| longitude        | float | The longitude of the lightning strike.                               |
| dateTimeUtc      | int   | The date and time of the lightning strike in UTC.                    |
| dateTimeUtcStr   | str   | The date and time of the lightning strike in UTC as a string.        |
| dateTimeLocalStr | str   | The date and time of the lightning strike in local time as a string. |
