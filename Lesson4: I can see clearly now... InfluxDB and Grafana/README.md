#Lesson 4: I can see clearly now… InfluxDB and Grafana
Goal: Add the InfluxDB plugin and view your test results using Grafana

This next step will involve adding dependencies to the package.json so that the testing Lambda can write results to InfluxDB.

###Step 1: Create a custom service for your tests

This greater level of customization allows the modification of the code which runs in AWS Lambda.

```sh
$ mkdir customTestLambda
$ cd customTestLambda
$ cp ../script.yml .
$ slsart configure
$ ls
handler.js	package.json    serverless.yml
```

(Note you may also see a script.yml if you've previously created that file.)

The purposes of these files follow:

|file|description|
|:----|:----------|
|package.json|Node.js dependencies for the Lambda.  Add Artillery plugins you want to use here.|
|serverless.yml|Serverless service definition. Change AWS-specific settings here|
|handler.js|Code to implement the load testing. **EDIT AT YOUR OWN RISK**|

From now on, slsart deploy and run will use these configuration files when run in this directory.  To use the originals, switch to a directory without a `serverless.yml`.

This entire directory is uploaded to AWS when the Lambda is deployed. This allows you to add plugins or payload files (*.csv).  Make sure that after any modifications to any of the files or the addition of new files, that you re-deploy with:

```sh
slsart deploy
```

Optionally, it should be possible to test that the current directory configuration is working with:

```sh
$ slsart deploy
$ slsart invoke -s script.yml
```

This should deploy and invoke the lambda using the local `./script.yml`.

###Step 2: Add influxdb Artillery plugin

To allow the Lambda code to write to InfluxDB, the correct NPM package dependency must be added. Run the following command (no -g global flag!) in the directory just created:

```sh
npm install --save artillery-plugin-influxdb
```

This modifies the package.json file to include the necessary dependency. The package.json file should now contain all these dependencies (version numbers may vary):

```JSON
{
  "dependencies": {
    "artillery-core": "^2.0.3-0",
    "artillery-plugin-influxdb": "^0.6.1",
    "csv-parse": "^1.1.7"
  }
}
```

###Step 3: Update Script to Log to Influx Server


Update the `config` portion of the test script to add the `plugin` from the example below:

```sh
  config:
    plugins:
      influxdb:
        testName: "<TEST_CASE_NAME>"  # This name must be changed
        influx:
          host: "http://ec2-54-152-15-245.compute-1.amazonaws.com/"
          username: "admin"
          password: "admin"
          database: "artillery_metrics"

```

Lambda now has dependencies added to the node_modules directory, so it's necessary to upload upload it again.
Then it can run again with the newly updated script:

```sh
$ slsart deploy
$ slsart invoke -s script.yml
```

If all went correctly, the load test data was added to the InfluxDB. Next step is to query the DB.

###Step 4: Query and Visualize the Results

The database containing the results should have already been created, and is referenced in the test script under the `influx` part. 
In this example, the database `artillery_metrics` is used.


Log into InfluxDB at: [http://ec2-54-161-98-139.compute-1.amazonaws.com/:8083/](http://ec2-54-161-98-139.compute-1.amazonaws.com:8083/) and perform a quick query to check that database exists:

```
SHOW DATABASES
```

The `artillery_metrics` database shold be listed. In the InfluxDB dashboard, select the `artillery_metrics` database from the drop-down list. 
With that selection made, queries made will be against that database.
 
To see the measurements stored in this database, run this command:
  
```
SHOW MEASUREMENTS
```  

The `latency` measurement should be in the list. To show all of the latencies, select them all:

```
SELECT * FROM latency WHERE
```

To see only results from a specific test, run:
 
```
SAELECT * FROM latency WHERE testName = 'a09y-smoke-load-test'
```

Once the test results have been verified in InfluxDB, it's time to see the graphs in Grafana.

Log in using `admin/admin` for the username and password and open the `Load Test Results` dashboard. 
Once on the dashboad, pick the test name from the drop-down list, make sure that the time-span includes the test results above.
 
There will be a visualization of the test results, including latencies load and errors.

![Load Test Dashboard](https://github.com/Nordstrom/serverless-artillery-workshop/blob/master/Images/grafana-dashboard.jpg)

####Optional:

Set Grafana to update every 10 seconds and show metrics from the last minute or so. Return to the console and run the tests again, 
perhaps increasing the test duration to a minute long or more.

Switch back to the Grafana dashboard and watch the test results in real-time!

