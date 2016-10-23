#Lesson 2: Aiming your artillery
Goal: create a script and test your own service endpoint

###Step 1: Create a simple load script with a short duration and small load (<25 TPS).

```
$ slsart script --endpoint <complete target URL here> --duration 10 --rate 5 --rampTo 15
$ slsart run
```

###Step 2: Let's take a look at the script that was created.

```
$ ls
$ <your fav editor> script.yml
```

This is the file you will modify to describe your load test the script feature is used only to quickly create a basic script for you to run from.

The load script determines what targets are load tested and how.  Artillery.io's configuration script is fully documented on their web page - https://artillery.io/docs/.  Lots of examples can be found at https://github.com/shoreditch-ops/artillery-core/tree/master/test/scripts.

Before we do too much customization, let's take a look at cloudwatch and setup reporting to InfluxDB in Lessons 3 and 4.
