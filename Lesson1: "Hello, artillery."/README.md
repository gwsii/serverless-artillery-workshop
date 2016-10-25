#Lesson 1: “Hello, artillery.”
Goal: Deploy and run a simple load test against a public endpoint.

###Prerequisites
We assume you have [Node.js](https://nodejs.org/en/) (v4 or better) installed.

###Step 1: serverless-artillery requires AWS credentials

####Option 1:
Go to AWS IAM console --> users --> select your user ID --> security credentials tab
Select: Create Access Key
Download credentials csv file

```sh
<editor of choice> ~/.aws/credentials
```

Add to the credentials file:
```sh
[my-profile]
aws_access_key_id=<your access key ID from the credentials csv>
aws_secret_access_key=<your secret access key from the credentials csv>
```

From your terminal:
```sh
$ export AWS_PROFILE=my-profile
```

####Option 2:
You may already have these credentials on your machine using the AWS SDK, aws init, or some corporate utility.

```sh
$ export AWS_PROFILE=your-preexisting-profile
```

####Option 3:
Grab your credentials from a script, tool, or whatevs and add them to the environment.

```sh
$ export AWS_ACCESS_KEY_ID=<access-key-id>
$ export AWS_SECRET_ACCESS_KEY=<secret-access-key>
$ export AWS_SESSION_TOKEN=<session-token>             # this one is optional
```

###Step 2: install serverless v1.0.3+ and the serverless-artillery node package on your machine

####Note: if you are on a VPN and use a proxy, export your proxy to your shell
```sh
export proxy=https://your.proxy.com:1234
```

Regardless, install the the things
```sh
$ sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share} # this is for those of you who have corrupted your file system
$ npm install -g serverless
$ npm install -g serverless-artillery
```

###Step 3: create a new load testing Lambda in your AWS account 
```sh
$ slsart deploy
```
Check your AWS console lambda page to confirm that a new Lambda has been created, this can take a minute for the page to update even though the Lambda is available.

###Step 4: Without script parameters, slsart invoke will run the lambda with a built-in default load script - a short test against https://aws.amazon.com with low load
```sh
$ slsart invoke
```

###Step 5: after ~5 seconds, you should see the results returned directly in the CLI
Scroll to the top of the results output to see the summary
This (seeing load in the CLI) will only be true for short loads (<1 min 58 sec) and small rates (<25 RPS)
For larger loads you'll need metric collection on your service or a results plug-in and a results database (we'll cover this in later lessons).

###Step 6: in the AWS console, check out your Cloud Watch logs
In AWS console --> Lambda --> select your lambda function
Select monitoring tab --> click on the relevant graph (like invocations)
If you see errors, check the Cloud Watch logs of your Lambda function for specifics.
