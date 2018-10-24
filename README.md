# Sensu InfluxDB Handler
TravisCI: [![TravisCI Build Status](https://travis-ci.org/nikkiki/sensu-influxdb-handler.svg?branch=master)](https://travis-ci.org/nikkiki/sensu-influxdb-handler)

The Sensu InfluxDB Handler is a [Sensu Event Handler][3] that sends metrics to
the time series database [InfluxDB][2]. [Sensu][1] can collect metrics using
check output metric extraction or the StatsD listener. Those collected metrics
pass through the event pipeline, allowing Sensu to deliver the metrics to the
configured metric event handlers. This InfluxDB handler will allow you to
store, instrument, and visualize the metric data from Sensu.

Check out [The Sensu Blog][5] for a step by step guide!

## Installation

Download the latest version of the sensu-influxdb-handler from [releases][4],
or create an executable script from this source.

From the local path of the sensu-influxdb-handler repository:
```
go build -o /usr/local/bin/sensu-influxdb-handler main.go
```

## Configuration

Example Sensu 2.x handler definition:
```
{
  "name": "influx-db",
  "type": "pipe",
  "command": "sensu-influxdb-handler --addr 'http://123.4.5.6:8086' --username 'foo' --password 'bar' --db-name 'myDB'"
}
```

Example Sensu 2.x check definition:
```
{
  "name": "collect-metrics",
  "command": "collect.sh",
  "interval": 10,
  "subscriptions": [
    "system"
  ],
  "output_metric_format": "graphite_plaintext",
  "output_metric_handlers": ["influx-db"]
}
```
That's right, you can collect different types of metrics (ex. Graphite), Sensu
will extract and transform them, and this handler will populate them into your
InfluxDB.

## Usage Examples

Help:
```
Usage:
  sensu-influxdb-handler [flags]

Flags:
  -a, --addr string       the address of the influx-db server, should be of the form 'http://host:port'
  -d, --db-name string    the influx-db to send metrics to
  -h, --help              help for handler-influx-db
  -p, --password string   the password for the given db
  -u, --username string   the username for the given db
```

## Contributing

nikkiki/sensu-influxdb-handler requires the Developer Certificate of Origin (DCO)
process to be followed.

The DCO is an attestation attached to every contribution made by every
developer. In the commit message of the contribution, the developer
simply adds a Signed-off-by statement and thereby agrees to the [DCO][6].

```
Author: Nikki Attea <nikki@sensu.io>

 Committer: Nikki Attea <nikki@sensu.io>

   Winter is coming.

   Signed-off-by: Nikki Attea <nikki@sensu.io>
```

Git makes this easy with git commit --signoff! The DCO text can either be
manually added to your commit body, or you can add either -s or --signoff
to your usual git commit commands.

[1]: https://github.com/sensu/sensu-go
[2]: https://github.com/influxdata/influxdb
[3]: https://docs.sensu.io/sensu-core/2.0/reference/handlers/#how-do-sensu-handlers-work
[4]: https://github.com/nikkiki/sensu-influxdb-handler/releases
[5]: https://blog.sensu.io/check-output-metric-extraction-with-influxdb-grafana
[6]: http://developercertificate.org/
