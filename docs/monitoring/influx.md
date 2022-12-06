# Local InfluxDB + GrafAna Setup

## Links
The following is only accessible from the internal university network.

- [InfluxDB](http://eplvm003.ph.bham.ac.uk:8086)
- [GrafAna](http://eplvm003.ph.bham.ac.uk:3000)

## GrafAna Data Sources
The Flux language employed by InfluxDB v2 is not fully supported by GrafAna. The easiest way to bypass this is to create a [virtual DataBase and Retention Policy mapping](https://docs.influxdata.com/influxdb/cloud/query-data/influxql/dbrp/).