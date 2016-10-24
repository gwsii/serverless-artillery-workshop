#Lesson 3: Cloud watching your service
Goal: Use builtin cloudwatch metrics to see how your service is impacted by the load.

If you're just interested in a simple view of how load impacts your service, it may not be as important to analyze the details from the load generation side.

###Step 1: Take a look at your service's cloudwatch dashboards while under load.
Cloudwatch metrics on your services (ex: API Gateway, Lambda, DynamoDB, Elastic Beanstalk, EC2, etc) should update within a few minutes of receiving load.  Take a minute to look through your relevant metrics.

###Step 2: Create a cloudwatch dashboard.
Time invested in creating a dashboard is time well spent.  If you haven't already, take a moment to create one now. (http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Dashboards.html)
