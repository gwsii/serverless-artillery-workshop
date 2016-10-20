#Lesson 1: “Hello, artillery.”
Goal: Deploy and run a simple load test against a public endpoint.

###Prerequisites
Installation
We assume you have node.js (v4 or better) installed. Likewise you should have the serverless framework (v1.0+) either installed globally or available in the local node_modules.

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
You may already have these credentials on your machine using the AWS SDK and aws init.

###Step 2: install serverless v1.0.2+ and the serverless-artillery node package on your machine
```sh
$ sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}
$ npm install -g serverless
$ npm install -g serverless-artillery
```

###Step 3: create a new load testing Lambda in your AWS account 
```sh
$ slsart deploy
```
check your AWS console lambda page to confirm


###Step 4: by default, slsart run will briefly test against https://aws.amazon.com with low load
```sh
$ slsart run
```

###Step 5: you should see the results returned directly
scroll to the top of the results output to see the summary
this will only be true for short loads (<4 min) and small rates (<25 TPS)


###Step 6: in the AWS console, check out your cloudwatch logs
In AWS console --> Lambda --> select your lambda function
Select monitoring tab --> click on the relevant graph
