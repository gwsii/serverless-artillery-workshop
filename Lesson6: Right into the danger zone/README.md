#Lesson 6: Right into the danger zone
Goal: Understand how your system behaves under edge-cases, when concurrency and database limits are hit.

#####!!! Important Safety Notes !!!
* Serverless-artillery requires an AWS account and can run **hundreds or thousands** of AWS Lambda functions.  If you are already running AWS Lambda in production, please be aware of and understand your Lambda concurrency limits before using serverless-artillery.  If unsure, use a different AWS account from your production systems.
* You can easily generate **massive numbers** of transactions per second.  Please use this power responsibly.  We have set some soft limits (5,000 transactions per second and 12 hours) to help with this.
* Bugs and odd edge cases can result in Lambdas calling Lambdas calling Lambdas - monitor your AWS Lambda invocations during and after each run.  Understand how to revoke Lambdas (slsart remove) to stop runaway Lambda trains.
* AWS generally likes to know if you're launching a significant load test. They will also warm stuff up for you, which reduces throttling errors early in the test, meaning you don't have to throw as much data away.
* If you start a long load and want to cancel it, you must use slsart remove (or delete from the AWS Console) and then wait for the control lambda to finish its 4-minute run and fail to invoke the next lambda to 'stop the train'.


###Step 1:
Contest rules and prizes to be announced at the workshop. ;)