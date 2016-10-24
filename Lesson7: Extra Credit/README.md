#Lesson 7: Extra credit
Goal: A deeper understanding of the theory of the problem and the theory of the solution.

The following addition to your Artillery script can control the values that the project uses for validating scripts and determining how to split and distribute the script's declared load across Lambdas.

This was helpful for debugging.  Note that as programmed, the handler will allow these values to be reduced from their defaults but will reject increases in these values.  Increases thereby require editing and re-deploying the code.

```sh
{	# default values listed below
	_split: {
		maxScriptDurationInSeconds: 86400,
		maxChunkDurationInSeconds: 240,
		maxScriptRequestsPerSecond: 5000,
		maxChunkRequestsPerSecond: 25,
		timeBufferInMilliseconds: 15000
	}
}
```

###Step 1:
Configure your default lambda max load (`maxChunkRequestsPerSecond`) to 500, create a ramp from 1 to 500 over 240 seconds - what happens?  Why?

###Step 2:
Increase your default lambda power from 1024 to 1536 and repeat step 1.
Now decrease your default lambda power to 128 and repeat step 1 again.
Lambda power dictates CPU, IO, and RAM - what's happening here?  What's the best default for your endpoint?

###Step 3:
How would you create a distribution view (histogram, violin plot) of your latencies to better understand cold start behavior?

###Step 4:
How does your P99 change when you 'warm up' your serverless endpoint first?  Try redeploying your endpoint and creating a sharp step load - what do the initial latencies look like?  Then, after the endpoint is warmed try the same step again.  How long does the endpoint stay warmed?
