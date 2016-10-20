#Lesson 4: I can see clearly now… InfluxDB and Grafana
Goal: Add the InfluxDB plugin and view your test results using Grafana

###Step 1: Create a simple load script with a short duration and small load (<25 TPS).

```sh
$ npm install -g artillery-plugin-influxdb
$ slsart configure
$ <your fav editor> script.?
```

Normally, slsart deploy and run take advantage of a default set of configuration files created when you installed serverless-artillery.  By using the config option, you've created a copy of all of them in your current local directory.  From now on, slsart deploy and run will reference these ocnfiguraiton files.
They include:
* serverless.yaml
* package.json
* node modules
* load script (if not there already)

```sh
{
  "config": {
    "plugins": {
        "influxdb": {
            "testName": "my_load_test_case",
            "measurementName": "Latency",
            "errorMeasurementName": "ClientSideErrors",
            "testRunId": "342-233-221",
            "tags": {
                "environment": "joes-dev-box",
                "host": "joe-dev.somewhere.org"
            },
            "influx": {
                "host": "my.influx.server.com",
                "username": "joe_developer",
                "password": "1t`sA$3cr3t",
                "database": "load_test_results"
            }
        }
    }
  }
}
```


- <edit> script to include influx plugins in configuration, your own test name
- npm install - - save artillery-plugin-influxdb (modifies package.son to add dependency)
- slsart deploy
- slsart run
- Query InfluxDB
- Look at pretty pictures.