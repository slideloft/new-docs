---
title: Running
order: 40
---

# Running

Once your Expansion database is configured, you're ready to run Expansion. To run Expansion you simply run `Expansion` or `Expansion serve`, both of which start the HTTP server and start logging to standard out. When run, you should see output similar to:

```text
INFO[0000] Starting Expansion on :8000           pid=29013
```

The log line above announces that Expansion is ready to serve client requests. Note: the numbers shown above may be different for your installation. Next you can confirm that Expansion is responding correctly by loading the root resource. In the example above, that URL would be [http://127.0.0.1:8000/](http://127.0.0.1:8000/), and simply running `curl http://127.0.0.1:8000/` shows you that the root resource can be loaded correctly.

If you didn't set up a Bantu Core node yet, you may see an error like this:

```text
ERRO[2019-05-06T16:21:14.126+08:00] Error getting core latest ledger err="get failed: pq: relation \"ledgerheaders\" does not exist"
```

Expansion requires a functional Bantu Core node. Go back and set up Bantu Core as described in the [Run a Core Node guide](../run-core-node/index.md). In particular, you need to initialise the database as [described here](../run-core-node/configuring.md#buckets).

## Ingesting Live Bantu Core Data

Expansion provides most of its utility through ingested data. Your Expansion server can be configured to listen for and ingest transaction results from the connected Bantu Core instance.

To enable ingestion, you must either pass `--ingest=true` on the command line or set the `INGEST` environment variable to "true". As of Expansion 1.0.0, you can start multiple ingesting machines in your cluster.

### Ingesting Historical Data

To enable ingestion of historical data from Bantu Core, you need to run `Expansion db reingest range start end`. If you're running a [full validator](../run-core-node/index.md#full-validator) with published history archive, for example, you might want to ingest all of the network's history. You can run this process in the background while your Expansion server is up. This continuously decrements the `history.elder_ledger` in your /metrics endpoint until `NUM_LEDGERS` is reached and the backfill is complete.

### Ingesting Historical Data and Reingesting Ledgers

To reingest older ledgers — which you may need to do after a version upgrade — or to ingest ledgers closed by the network before you started Expansion use the `Expansion db reingest range [START_LEDGER] [END_LEDGER]` command:

```text
expansion1> expansion db reingest range 1 10000
expansion2> expansion db reingest range 10001 20000
expansion3> expansion db reingest range 20001 30000
# ... etc.
```

This allows reingestion to be split up and done in parallel by multiple Expansion processes.

### Managing Storage for Historical Data

Over time, the recorded network history will grow unbounded, increasing storage used by the database. Expansion needs sufficient disk space to expand the data ingested from Bantu Core. Unless you need to maintain a [history archive](../run-core-node/publishing-history-archives.md), you may configure Expansion to only retain a certain number of ledgers in the database. This is done using the `--history-retention-count` flag or the `HISTORY_RETENTION_COUNT` environment variable. Set the value to the number of recent ledgers you wish to keep around, and every hour the Expansion subsystem will reap expired data. Alternatively, you may execute the command `Expansion db reap` to force a collection.

### Surviving Bantu Core Downtime

Expansion tries to maintain a gap-free window into the history of the Bantu network. This reduces the number of edge cases that Expansion-dependent software must deal with in an attempt to make the integration process simpler. To maintain a gap-free history, Expansion needs access to all of the metadata produced by Bantu Core in the process of closing a ledger, and there are instances when this metadata can be lost. Usually, this loss of metadata occurs because the Bantu Core node went offline and performed a catchup operation when restarted.

To ensure that the metadata required by Expansion is maintained, you have several options: You may either set the `CATCHUP_COMPLETE` Bantu Core configuration option to `true` or configure `CATCHUP_RECENT` to determine the amount of time your Bantu Core can be offline without having to rebuild your Expansion database.

Unless your node is a [Full Validator which publishes an archive](../run-core-node/index.md#full-validator) we _do not_ recommend using the `CATCHUP_COMPLETE` method, as this will force Bantu Core to apply every transaction from the beginning of the ledger, which will take an ever increasing amount of time. Instead, we recommend you set the `CATCHUP_RECENT` config value. To do this, determine how long of a downtime you would like to survive \(expressed in seconds\) and divide by ten. This roughly equates to the number of ledgers that occur within your desired grace period since ledgers roughly close at a rate of one every ten seconds. With this value set, Bantu Core will replay transactions for ledgers that are recent enough, ensuring that the metadata needed by Expansion is present.

### Correcting Gaps in Historical Data

In the section above, we mentioned that Expansion _tries_ to maintain a gap-free window. Unfortunately, it cannot directly control the state of Bantu-core and [so gaps may form](https://www.Bantu.org/developers/software/known-issues.html#gaps-detected) due to extended down time. When a gap is encountered, Expansion will stop ingesting historical data and complain loudly in the log with error messages \(log lines will include "ledger gap detected"\). To resolve this situation, you must re-establish the expected state of the Bantu Core database and purge historical data from Expansion's database. We leave the details of this process up to the reader as it is dependent upon your operating needs and configuration, but we offer one potential solution:

We recommend you configure the HISTORY\_RETENTION\_COUNT in Expansion to a value less than or equal to the configured value for CATCHUP\_RECENT in Bantu Core. Given this situation, any downtime that would cause a ledger gap will require a downtime greater than the amount of historical data retained by Expansion. To re-establish continuity:

1. Stop Expansion.
2. Run `Expansion db reap` to clear the historical database.
3. Clear the cursor for Expansion by running `Bantu-core -c "dropcursor?id=Expansion"` \(ensure capitilization is maintained\).
4. Clear ledger metadata from before the gap by running `Bantu-core -c "maintenance?queue=true"`.
5. Restart Expansion.

### Some endpoints are not available during state ingestion

Endpoints that display state information are not available during initial state ingestion and will return a `503 Service Unavailable`/`Still Ingesting` error. An example is the `/paths` endpoint \(built using offers\). Such endpoints will become available after state ingestion is done \(usually within a couple of minutes\).

### State ingestion is taking a lot of time

State ingestion shouldn't take more than a couple of minutes on an AWS `c5.xlarge` instance, or equivalent.

It's possible that the progress logs \(see below\) will not show anything new for a longer period of time or print a lot of progress entries every few seconds. This happens because of the way history archives are designed. The ingestion is still working but it's processing entries of type `DEADENTRY`'. If there is a lot of them in the bucket, there are no _active_ entries to process. We plan to improve the progress logs to display actual percentage progress so it's easier to estimate ETA.

If you see that ingestion is not proceeding for a very long period of time:

1. Check the RAM usage on the machine. It's possible that system ran out of RAM and it using swap memory that is extremely slow.
2. If above is not the case, file a new issue in [the Expansion repository](https://github.com/Bantu/go/tree/master/services/Expansion).

### CPU usage goes high every few minutes

This is _by design_. Expansion runs a state verifier routine that compares state in local storage to history archives every 64 ledgers to ensure data changes are applied correctly. If data corruption is detected, Expansion will block access to endpoints serving invalid data.

We recommend keeping this security feature turned on; however, if it's causing problems \(due to CPU usage\) this can be disabled by `--ingest-disable-state-verification` CLI param or `INGEST-DISABLE-STATE-VERIFICATION` env variable.

### I see `Waiting for the next checkpoint...` messages

If you were running the new system in the past during experimental stage \(`ENABLE_EXPERIMENTAL_INGESTION` flag\) it's possible that the old and new systems are not in sync. In such case, the upgrade code will activate and will make sure the data is in sync. When this happens you may see `Waiting for the next checkpoint...` messages for up to 5 minutes.

## Reading the logs

In order to check the progress and the status of experimental ingestion you should check the logs. All logs connected to experimental ingestion are tagged with `service=expingest`.

It starts with informing you about state ingestion:

```text
INFO[2019-08-29T13:04:13.473+02:00] Starting ingestion system from empty state...  pid=5965 service=expingest temp_set="*io.MemoryTempSet"
INFO[2019-08-29T13:04:15.263+02:00] Reading from History Archive Snapshot         ledger=25565887 pid=5965 service=expingest
```

During state ingestion, Expansion will log number of processed entries every 100,000 entries \(there are currently around 7M entries in the public network\):

```text
INFO[2019-08-29T13:04:34.652+02:00] Processing entries from History Archive Snapshot  ledger=25565887 numEntries=100000 pid=5965 service=expingest
INFO[2019-08-29T13:04:38.487+02:00] Processing entries from History Archive Snapshot  ledger=25565887 numEntries=200000 pid=5965 service=expingest
INFO[2019-08-29T13:04:41.322+02:00] Processing entries from History Archive Snapshot  ledger=25565887 numEntries=300000 pid=5965 service=expingest
INFO[2019-08-29T13:04:48.429+02:00] Processing entries from History Archive Snapshot  ledger=25565887 numEntries=400000 pid=5965 service=expingest
INFO[2019-08-29T13:05:00.306+02:00] Processing entries from History Archive Snapshot  ledger=25565887 numEntries=500000 pid=5965 service=expingest
```

When state ingestion is finished, it will proceed to ledger ingestion starting from the next ledger after checkpoint ledger \(25565887+1 in this example\) to update the state using transaction meta:

```text
INFO[2019-08-29T13:39:41.590+02:00] Processing entries from History Archive Snapshot  ledger=25565887 numEntries=5300000 pid=5965 service=expingest
INFO[2019-08-29T13:39:44.518+02:00] Processing entries from History Archive Snapshot  ledger=25565887 numEntries=5400000 pid=5965 service=expingest
INFO[2019-08-29T13:39:47.488+02:00] Processing entries from History Archive Snapshot  ledger=25565887 numEntries=5500000 pid=5965 service=expingest
INFO[2019-08-29T13:40:00.670+02:00] Processed ledger                              ledger=25565887 pid=5965 service=expingest type=state_pipeline
INFO[2019-08-29T13:40:00.670+02:00] Finished processing History Archive Snapshot  duration=2145.337575904 ledger=25565887 numEntries=5529931 pid=5965 service=expingest shutdown=false
INFO[2019-08-29T13:40:00.693+02:00] Reading new ledger                            ledger=25565888 pid=5965 service=expingest
INFO[2019-08-29T13:40:00.694+02:00] Processing ledger                             ledger=25565888 pid=5965 service=expingest type=ledger_pipeline updating_database=true
INFO[2019-08-29T13:40:00.779+02:00] Processed ledger                              ledger=25565888 pid=5965 service=expingest type=ledger_pipeline
INFO[2019-08-29T13:40:00.779+02:00] Finished processing ledger                    duration=0.086024492 ledger=25565888 pid=5965 service=expingest shutdown=false transactions=14
INFO[2019-08-29T13:40:00.815+02:00] Reading new ledger                            ledger=25565889 pid=5965 service=expingest
INFO[2019-08-29T13:40:00.816+02:00] Processing ledger                             ledger=25565889 pid=5965 service=expingest type=ledger_pipeline updating_database=true
INFO[2019-08-29T13:40:00.881+02:00] Processed ledger                              ledger=25565889 pid=5965 service=expingest type=ledger_pipeline
INFO[2019-08-29T13:40:00.881+02:00] Finished processing ledger                    duration=0.06619956 ledger=25565889 pid=5965 service=expingest shutdown=false transactions=29
INFO[2019-08-29T13:40:00.901+02:00] Reading new ledger                            ledger=25565890 pid=5965 service=expingest
INFO[2019-08-29T13:40:00.902+02:00] Processing ledger                             ledger=25565890 pid=5965 service=expingest type=ledger_pipeline updating_database=true
INFO[2019-08-29T13:40:00.972+02:00] Processed ledger                              ledger=25565890 pid=5965 service=expingest type=ledger_pipeline
INFO[2019-08-29T13:40:00.972+02:00] Finished processing ledger                    duration=0.071039012 ledger=25565890 pid=5965 service=expingest shutdown=false transactions=20
```

## Managing Stale Historical Data

Expansion ingests ledger data from a connected instance of Bantu Core. In the event that Bantu Core stops running \(or if Expansion stops ingesting data for any other reason\), the view provided by Expansion will start to lag behind reality. For simpler applications, this may be fine, but in many cases this lag is unacceptable and the application should not continue operating until the lag is resolved.

To help applications that cannot tolerate lag, Expansion provides a configurable "staleness" threshold. Given that enough lag has accumulated to surpass this threshold \(expressed in number of ledgers\), Expansion will only respond with an error: [`stale_history`](https://github.com/Bantu/go/blob/master/services/Expansion/internal/docs/reference/errors/stale-history.md). To configure this option, use either the `--history-stale-threshold` command line flag or the `HISTORY_STALE_THRESHOLD` environment variable. NOTE: non-historical requests \(such as submitting transactions or finding payment paths\) will not error out when the staleness threshold is surpassed.

