#Lesson 3: Cloud watching your service (could be serverless.com)
Goal: Use builtin cloudwatch metrics to see how your service is impacted by the load.

If you're just interested in a view of how load impacts your service, it's not as important to analyze the latency and return codes from the load generation side.

###Step 1: Take a look at your service's cloudwatch dashboards while under load.
Cloudwatch metrics on your service (ex: API Gateway, Lambda, DynamoDB, etc) should update within a few minutes of receiving load.  Take a minute to look through your metrics and create a dashboard.