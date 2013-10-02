![](https://flood.io/assets/flood-logo.png)

### Performance Benchmarks from flood.io

Here at Flood IO we love performance testing. Since we support multiple tools including JMeter and Gatling, we think it's best if we keep track of individual tool performance via different benchmarks. You can see the test plans used for benchmarking for __[Gatling](./benchmarks/spec/gatling.scala)__ and __[JMeter](./benchmarks/spec/jmeter.jmx)__.

We're not in the business of playing one tool off the other, we think different tools meet different requirements of our testers. After all, _"all competitive benchmarking is institutionalized cheating."_ [Guerrilla Manifesto](http://www.perfdynamics.com/Manifesto/gcaprules.html#tth_sEc1.21)

As we benchmark the tools in different load scenarios and test configurations we'll document the raw results here for your own analysis. This includes things like GC behvaviour under load, as well as links to summary reports from tests executed on __[flood.io](https://flood.io)__. It's interesting to see how tools behave in high load scenarios. "High" meaning bigger than your own laptop :)

Our basic benchmark consists of throwing __10,000__ users at an __nginx__ site for 30 minutes duration with a [scenario](./benchmarks/spec/scenario.md) that GETs a slow resource (3.5s) 20% of the time, cacheable content (< 10ms) 40% of the time, non-cacheable content (2s) 30% of the time and and the rest simulated POSTs (4s). Each scenario will parse the response (for a string using regular expressions) as well as body and response code assertions. [Apdex](http://apdex.org) is measured on a 4000 ms satisfied target. 

The target site and flood.io node are separate AWS instances (m1.xlarge) located in the same region (Sydney). The JVM heap size max is 6GB typically run with the following settings:

```
java -server -XX:+HeapDumpOnOutOfMemoryError 
-Xms6144m -Xmx6144m -XX:NewSize=1536m -XX:MaxNewSize=1536m 
-XX:MaxTenuringThreshold=2 -XX:+UseConcMarkSweepGC 
-Dsun.rmi.dgc.client.gcInterval=600000 
-Dsun.rmi.dgc.server.gcInterval=600000 
-XX:PermSize=64m -XX:MaxPermSize=128m 
-verbose:gc 
-XX:+PrintGCDateStamps 
-XX:+PrintGCTimeStamps 
-XX:+PrintGCDetails
-Xloggc:/var/log/flood/verbosegc.log  -XX:-UseGCLogFileRotation
```

We also include the __[test lab setup](./sites)__ (cloudformation templates) that can be used to replicate testing using your own AWS account. 

We hope you find this information useful. Questions about the testing can be sent to support@flood.io or please raise an issue against this repo for discussion. You can read [more about this benchmarking here.](https://flood.io/blog/11-benchmarking-jmeter-and-gatling)

Enjoy!

Tim Koopmans

latest benchmarks
==============
You can always get the latest current benchmark results from [flood.io](https://flood.io) at:

* __JMeter__ [RELEASE](https://flood.io/benchmarks/jmeter) [LATEST](https://flood.io/benchmarks/jmeter?version=latest)   
* __Gatling__ [RELEASE](https://flood.io/benchmarks/gatling) [LATEST](https://flood.io/benchmarks/gatling?version=latest)  

previous benchmarks
==============

| Benchmark  | Users        | Date                         | Apdex | Mean RT    |
| -----      |-----         |-----                         |-----  |-----       |
| [:chart_with_upwards_trend:](./benchmarks/results/e639303fb162ce.md) [:link:](https://flood.io/e639303fb162ce) Gatling-1.5.3    | 10000  | 20 mins<br>2013-09-30 09:52:32| 0.95 [4000] | 1788 ms |
| [:chart_with_upwards_trend:](./benchmarks/results/e281b0e339fb14.md) [:link:](https://flood.io/e281b0e339fb14) JMeter-2.9       | 10000  | 20 mins<br>2013-09-30 10:13:15| 0.95 [4000] | 1625 ms |
| [:chart_with_upwards_trend:](./benchmarks/results/9fde49a2f3d43b.md) [:link:](https://flood.io/9fde49a2f3d43b) JMeter-2.10      | 10000  | 20 mins<br>2013-09-30 10:33:59| 0.95 [4000] | 1698 ms |
| [:chart_with_upwards_trend:](./benchmarks/results/2037deb43774de.md) [:link:](https://flood.io/2037deb43774de) JMeter-2.9       | 20000  | 20 mins<br>2013-10-01 08:20:47| 0.87 [4000] | 2637 ms |
| [:chart_with_upwards_trend:](./benchmarks/results/57b90939e21846.md) [:link:](https://flood.io/57b90939e21846) JMeter-2.10      | 20000  | 20 mins<br>2013-10-01 08:41:49| 0.91 [4000] | 2143 ms |
| [:chart_with_upwards_trend:](./benchmarks/results/6666b6bc4cb8a2.md) [:link:](https://flood.io/6666b6bc4cb8a2) Gatling-1.5.3    | 20000  | 20 mins<br>2013-10-01 09:03:03| 0.95 [4000] | 1702 ms |
| [:chart_with_upwards_trend:](./benchmarks/results/2c13788664d83d.md) [:link:](https://flood.io/2c13788664d83d) Gatling-1.5.3    | 40000  | 20 mins<br>2013-10-01 09:53:57| 0.95 [4000] | 1574 ms |
| [:chart_with_upwards_trend:](./benchmarks/results/5bdd2601b9fb3c.md) [:link:](https://flood.io/5bdd2601b9fb3c) Gatling-1.5.3    |  100   | 2 mins<br>2013-10-02 10:29:33|  0.93 [4000] | 1931 ms |
| [:chart_with_upwards_trend:](./benchmarks/results/4ab9feb117064d.md) [:link:](https://flood.io/4ab9feb117064d) JMeter-2.9       |  100   | 2 mins<br>2013-10-02 10:32:10|  0.97 [4000] | 1130 ms |
| [:chart_with_upwards_trend:](./benchmarks/results/a7d55f2a8d313b.md) [:link:](https://flood.io/a7d55f2a8d313b) JMeter-r1528295  |  100   | 2 mins<br>2013-10-02 10:35:14| 0.96 [4000] | 1600 ms |
| [:chart_with_upwards_trend:](./benchmarks/results/9d32af84735887.md) [:link:](https://flood.io/9d32af84735887) Gatling-2.0.0-20131001.201622-332-bundle | 100 |2 mins<br>2013-10-02 10:37:44 | 0.96 [4000] | 1638 ms |
