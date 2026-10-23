# Synthetic Spatio-Temporal Datasets

This repository contains three small synthetic spatio-temporal datasets representing different data types (https://arxiv.org/pdf/1906.04928) commonly encountered in spatio-temporal analysis.

The datasets were created for testing and demonstrating spatio-temporal data-processing and feature-extraction workflows of the python library (st_feat - currently under development).

All records are synthetic and do not represent real people, real sensor measurements, or real-world reported events. For all three datasets, the spatial coordinates are intended as ordinary geographic longitude/latitude coordinates in WGS 84, i.e. EPSG:4326.

## Files

| File | Data type | Records | Main characteristics |
|---|---|---:|---|
| `synthetic_pointref.csv` | Point-reference | 480 | 10 moving sensors, 16 timestamps, directional measurements |
| `synthetic_raster.csv` | Raster-like | 20,160 | 60 fixed sensors' spatial locations, 336 hourly timestamps |
| `synthetic_event.csv` | Event | 100 | Timestamped categorical events at spatial locations |

---

## 1. Point-Reference Dataset

File: `synthetic_pointref.csv`

This file contains **480 observations** from **10 synthetic moving sensors**.

The data covers **16 timestamps** between:

- Start: `2026-01-01T00:00:00+00:00`
- End: `2026-01-02T12:00:00+00:00`

Each sensor contributes three directional observations at each timestamp, giving:

```text
10 sensors × 16 timestamps × 3 directions = 480 observations
```

The sensor coordinates do vary over time, allowing the dataset to represent point-reference observations with changing spatial positions.

### Columns

```csv
sensor_id,l1,l2,a,t,value
```

- `sensor_id`: identifier of the synthetic sensor (`S01`–`S10`).
- `l1`: first spatial coordinate (longitude).
- `l2`: second spatial coordinate (latitude).
- `a`: directional/orientation angle associated with the observation, in degrees.
- `t`: observation timestamp in UTC.
- `value`: synthetic numerical measurement.

### Example

```csv
S01,7.039737438173713,50.718819103676516,173.3612325498296,2026-01-01T00:00:00+00:00,17.143445557219138
```

### Data characteristics

- Number of records: `480`
- Number of sensors: `10`
- Number of unique timestamps: `16`
- Measurements per sensor: `48`
- Missing values: `0`
- Value range: approximately `15.11` to `22.88`

---

## 2. Raster Dataset

File: `synthetic_raster.csv`

The raster dataset contains synthetic values observed repeatedly at **60 fixed sensors' spatial locations** over **336 hourly timestamps**. It therefore contains:

```text
60 spatial locations × 336 timestamps = 20,160 observations
```

The temporal coverage is:

- Start: `2026-01-05T00:00:00+00:00`
- End: `2026-01-18T23:00:00+00:00`
- Temporal resolution: `1 hour`
- Duration: `14 days`


### Columns

```csv
l1,l2,t,value
```

- `l1`: first spatial coordinate (longitude).
- `l2`: second spatial coordinate (latitude).
- `t`: observation timestamp in UTC.
- `value`: synthetic numerical value at the corresponding location and time.

### Example

```csv
7.155431542683052,50.71600694175627,2026-01-05T01:00:00+00:00,32.730612407436574
```

### Data characteristics

- Number of records: `20,160`
- Number of spatial locations: `60`
- Number of timestamps: `336`
- Temporal resolution: `1 hour`
- Missing `value` entries: `401`
- Non-missing value range: approximately `12.56` to `100.41`

Missing entries are stored as empty values in the CSV and are interpreted as `NaN` by tools such as pandas.

---

## 3. Event Dataset

File: `synthetic_event.csv`

The event dataset represents discrete synthetic events occurring at particular locations and times. It contains **100 events** with spatial coordinates, timestamps, categorical event labels, and associated numerical values.

The temporal coverage is:

- Start: `2024-01-01T00:00:00+00:00`
- End: `2024-03-07T00:00:00+00:00`


### Columns

```csv
long,lat,time,event_type,value
```

- `long`: longitude of the synthetic event location.
- `lat`: latitude of the synthetic event location.
- `time`: event timestamp in UTC.
- `event_type`: synthetic categorical event label.
- `value`: numerical quantity associated with the event.

### Example

```csv
7.1,50.7,2024-01-01T00:00:00+00:00,theft,2.0
```

### Data characteristics

- Number of records: `100`
- Number of unique timestamps: `100`
- Number of event categories: `2`
- Event categories: `theft`, `assault`
- Missing values: `0`

---

## Timestamp Format

Timestamps are represented using ISO 8601 notation with a UTC offset, for example:

```text
2026-01-05T10:00:00+00:00
```

Some timestamps in the point-reference dataset contain fractional-second precision.

---


## Intended Use

These datasets are designed as lightweight synthetic examples for developing, testing, and demonstrating statistical feature extraction utility of the software st_feat (under development).

Example tasks include - temporal and spatial descriptive statistics like:
- nearest-neighbor and neighborhood statistics,
- covariance analysis,
- kernel pca,
- gaussian processes for uncertainity, 
- missing-data handling, etc.

## Notes

- All three datasets are **fully synthetic**.
- No personal information or tracked individuals are included.
- Event labels and locations are illustrative and do not describe real incidents.
- The datasets are intended primarily for research, software testing, demonstrations, and reproducible examples.
