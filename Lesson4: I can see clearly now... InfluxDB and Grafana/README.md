#Lesson 4: I can see clearly now… InfluxDB and Grafana
Goal: Add the InfluxDB plugin and view your test results using Grafana

This next step will involve adding dependencies to the package.json so that the testing Lambda can write results to InfluxDB.

###Step 1: Create a custom service for your tests

This greater level of customization allows the modification of the code which runs in AWS Lambda.

```sh
$ mkdir customTestLambda
$ cd customTestLambda
$ slsart configure
$ ls
handler.js	package.json	serverless.yml
```

The purposes of these files follow:

|file|description|
|:----|:----------|
|package.json|NodeJS dependencies for the Lambda.  Add Artillery plugins you want to use here.|
|serverless.yml|Serverless service definition. Change AWS-specific settings here|
|handler.js|Code to implement the load testing. **EDIT AT YOUR OWN RISK**|

From now on, slsart deploy and run will use these configuration files when run in this directory.  To use the originals, switch to a directory without a `serverless.yml`.

This entire directory is uploaded to AWS when the Lambda is deployed. This allows you to add plugins or payload files (*.csv).  May sure that after any modifications of any of the files or the addition of new files, that you re-deploy with:

```sh
slsart deploy
```

Optionally, it should be possible to test that the current directory configuration is working with:

```sh
$ slsart deploy
$ slsart run
```

This should deploy and run the local `./script.yml` and show results.

###Step 2: Add influxdb Artillery plugin

To allow the Lambda code to write to InfluxDB, the correct NPM package dependency must be added. Run the following command in the directory just created:

```sh
npm install --save artillery-plugin-influxdb
```

This modifies the package.json file to include the necessary dependency. The package.json file should now contain all these dependencies (version numbers may vary):

```JSON
{
  "dependencies": {
    "artillery-core": "^2.0.3-0",
    "artillery-plugin-influxdb": "^0.6.1",
    "csv-parse": "^1.1.7",
    "ntp-client": "^0.5.3"
  }
}
```

###Step 3: Update Script to Log to Influx Server

TODO: Add workshop server address.

YAML Config to Add:

```sh
  config: 
    plugins: 
      influxdb: 
        testName: "my_load_test_case"
        measurementName: "Latency"
        errorMeasurementName: "ClientSideErrors"
        influx: 
          host: "my.influx.server.com"
          username: "joe_developer"
          password: "1t`sA$3cr3t"
          database: "load_test_results"


```

```sh
$ slsart deploy
$ slsart run -s script.yml
```

###Step 4: Query and Visualize the Results

Log into InfluxDB and query for your testName. See many data points.

TODO: Influx DB login URL

Log into Grafana, open Load Tests page, pick testName from the list.

TODO: Grafana login URL.

See results.

Optionally, keep Grafana open and rerun tests seeing results arrive in real-time.
