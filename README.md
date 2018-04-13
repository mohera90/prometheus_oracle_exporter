# Prometheus Oracle Exporter

A [Prometheus](https://prometheus.io/) exporter for Oracle.

The following metrics are exposed currently. Support for RAC (databasename and instancename added via lables)

- oracledb_exporter_last_scrape_duration_seconds
- oracledb_exporter_last_scrape_error
- oracledb_exporter_scrapes_total
- oracledb_uptime (days)
- oracledb_session (view v$session system/user active/passive)
- oracledb_sysmetric (view v$sysmetric
                  (Physical Read Total IO Requests Per Sec / Physical Write Total IO Requests Per Sec
                   Physical Read Total Bytes Per Sec / Physical Write Total Bytes Per Sec))
- oracledb_sysstat (view v$sysstat (parse count (total) / execute count / user commits / user rollbacks))
- oracledb_waitclass (view v$waitclass)
- oracledb_tablespace (tablespace total/free)
- oracledb_interconnect (view v$sysstat (gc cr blocks served / gc cr blocks flushed / gc cr blocks received))
- oracledb_recovery (percentage usage in FRA from V$RECOVERY_FILE_DEST)
- oracledb_redo (Redo log switches over last 5 min from v$log_history)
- oracledb_cachehitratio (Cache hit ratios (v$sysmetric)
- oracledb_up (Whether the Oracle server is up)
- oracledb_error (Errors parsed from the alert.log)
- oracledb_services (Active Oracle Services (v$active_services))
- oracledb_parameter (Configuration Parameters (v$parameter))
- oracledb_query (Self defined Queries in Configuration File)


The Oracle Alertlog file is scanned and the metrics are exposed as a gauge metric with a total occurence of the specific ORA.
Yo can define your on Queries and execute and scrape them

# Installation

Ensure that the configfile (oracle.conf) is set correctly before starting. You can add multiple instances, e.g. the ASM instance. It is even possible to run one Exporter for all your Databases, but this is not recommended. We use it in our Company because on one host multiple Instances are running.


```bash
export NLS_LANG=AMERICAN_AMERICA.UTF8
/path/to/binary -l log.level error -l web.listen-address 9161
```

## Usage

```bash
Usage of ./prometheus_oracle_exporter:
  -configfile string
      ConfigurationFile in YAML format. (default "oracle.conf")
  -web.listen-address string
      Address to listen on for web interface and telemetry. (default ":9161")
  -web.telemetry-path string
      Path under which to expose metrics. (default "/metrics")
```
