#Lesson 5: “Hello, serverless-artillery.”
Goal: Deploy and run a large-scale load test against your endpoint.

What happens when we go beyond the load a single lambda can easily generate?  Serverless-artillery invokes more worker lambdas to generate more load.  If the duration of the load needed goes beyond 4 minutes, a new controller lambda is invoked, which can in turn invoke more worker lambdas, and more controller lambdas over time.

When you're using multiple Lambdas over an extended period of time, each Lambda is generating its own results.  For this reason, a data collection resource like InfluxDB is essential to understanding the results of your run.

###Step 1:
Try a rate greater than 25 and/or a duration greater than 240 seconds.  We have implemented a soft limit of 5,000 transactions per second (the rate) and 12 hours (the duration).  For the purpose of this lab, let's set your duration to 300 seconds and your rate to 500 TPS.

###Step 2:
Go to your Grafana dashboard from Lesson 4 and check out the results.  If you are doing long ramps, there is a known bug with artillery that sometimes calculates ramps a bit long, so you may see short overlaps across the 4-minute boundary.

###Step 3:
Play around, try some larger and smaller loads, remember, if you start a long load and want to cancel it, you must use slsart remove (or delete from the AWS Console) and then wait for the control lambda to finish its 4-minute run and fail to invoke the next lambda to 'stop the train'.

