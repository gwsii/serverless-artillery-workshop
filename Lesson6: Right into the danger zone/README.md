#Lesson 6: Right into the danger zone
Goal: Understand how your system behaves under edge-cases, when concurrency and database limits are hit.

###Step 1:
What happens when you ask for more lambdas than your account limit supports?
In Cloud Watch, add lambda throttling to your dashboard, then attempt to invoke a very short duration, very high load scenario.
By default, AWS gives you 100 concurrent Lambdas, so try something higher than 2500 RPS.

###Step 2:
In your sample serverless architecture, keep track of API Gateway Throttled requests (429 errors) and DynamoDB read/write limits.  These two can be the source of challenges.

###Step 3:
Remember, when you've starting something too big, to remove your Lambda function use:
```sh
$ slsart remove
```
