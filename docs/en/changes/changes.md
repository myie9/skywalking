## 9.4.0

#### Project

#### OAP Server

* Add `ServerStatusService` in the core module to provide a new way to expose booting status to other modules.
* Adds Micrometer as a new component.(ID=141)
* Refactor session cache in MetricsPersistentWorker.
* Cache enhancement - don't read new metrics from database in minute dimensionality.

```
    // When
    // (1) the time bucket of the server's latest stability status is provided
    //     1.1 the OAP has booted successfully
    //     1.2 the current dimensionality is in minute.
    // (2) the metrics are from the time after the timeOfLatestStabilitySts
    // (3) the metrics don't exist in the cache
    // the kernel should NOT try to load it from the database.
    //
    // Notice, about condition (2),
    // for the specific minute of booted successfully, the metrics are expected to load from database when
    // it doesn't exist in the cache.
```

* Remove the offset of metric session timeout according to worker creation sequence.
* Correct `MetricsExtension` annotations declarations in manual entities.
* Support component IDs' priority in process relation metrics.
* Remove abandon logic in MergableBufferedData, which caused unexpected no-update.
* Fix miss set `LastUpdateTimestamp` that caused the metrics session to expire.
* Rename MAL rule `spring-sleuth.yaml` to `spring-micrometer.yaml`.
* Fix memory leak in Zipkin API.
* Remove the dependency of `refresh_interval` of ElasticSearch indices from `elasticsearch/flushInterval` config. Now,
  it uses `core/persistentPeriod` + 5s as `refresh_interval` for all indices instead.
* Change `elasticsearch/flushInterval` to 5s(was 15s).
* Optimize `flushInterval` of ElasticSearch BulkProcessor to avoid extra periodical flush in the continuous bulk streams. 
* An unexpected dot is added when exp is a pure metric name and expPrefix != null.
* Support monitoring MariaDB.
* Remove measure/stream specific interval settings in BanyanDB.
* Add global-specific settings used to override global configurations (e.g `segmentIntervalDays`, `blockIntervalHours`) in BanyanDB.
* Use TTL-driven interval settings for the `measure-default` group in BanyanDB.
* Fix wrong group of non time-relative metadata in BanyanDB.
* Refactor `StorageData#id` to the new StorageID object from a String type.

#### UI

#### Documentation

* Remove Spring Sleuth docs, and add `Spring MicroMeter Observations Analysis` with the latest Java agent side
  enhancement.
* Update `monitoring MySQL document` to add the `MariaDB` part.
* Reorganize the protocols docs to a more clear API docs.

All issues and pull requests are [here](https://github.com/apache/skywalking/milestone/160?closed=1)
