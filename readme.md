# ELK + FileBeat + MetricBeat + Curator
A working configuration to allow you to leverage ELK, MetricBeat and Curator to handle your logging.

By default, this will provided the ability to configure filebeat for straight docker log parsing from the local docker agent, as well as default metricbeat indexes and dashboard/visualizations to easily view metrics of your local docker containers.

NOTE: This does NOT work on mac.  You can only leverage this on a linux machine or windows machine.  There are issues with exposes the required data via a mac through the VM which limits the ability to test this locally on a mac.

`ElasticSearch` - elastic search leveraged for piping your data into an easily indexable format

`Logstash` - this part is NOT configured, but you can easily expand this project to have more precise logging and analytics

`Kibana` - a ui for configuration, management, visualization, dashboards and more

Beats used:

`FileBeat` - used to parse the docker json log files for quick log indexing and search without.  Leverage logstash to properly configure more powerful and insightful logging

`MetricBeat` - used to parse metrics from various technologies, in this case Docker specific metrics for the local Docker instance

# Pre-reqs

- create a local `.env` file in this project with your own values like below:

```
ELK_VERSION=7.7.1
ELASTICSEARCH_HOSTS="http://elasticsearch:9200"
ELASTICSEARCH_USERNAME=elastic
ELASTICSEARCH_PASSWORD=elastic
KIBANA_HOST="http://kibana:5601"
```

# Starting up ELK + Metric Beat and Curator

## start original ELK stack

- `docker-compose up -d`

## start up curator

Modify the run.sh under the `curator` directory with your desired cron job pattern.  The default value in place of `30 4 * * *` will run the curator tasks every day at 4:30pm EST once the container is started.  If you need help with cron format then check out [Cron Tab Guru](https://crontab.guru/)