#Work in progress.  Don't believe everything you read.

#Lesson 5: “Hello, serverless-artillery.”
Goal: Deploy and run a large-scale load test against your endpoint.


What happens when we go beyond the load a single lambda can easily generate?  Serverless-artillery invokes more worker lambdas to generate more load.  If the duration of the load needed goes beyond 4 minutes, a new controller lambda is invoked, which can in turn invoke more worker lambdas, and more controller lambdas over time.

Try a rate greater than 25 and a duration greater than 240 seconds.