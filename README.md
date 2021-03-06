# Label supported JMX metrics
Provides an object name factory for Dropwizard that adds the support for metric labels.
Labels are of great value for example on aggregating metrics by Prometheus.

### Sample Usage

The client code for referring to a labeled metric is like this:

```java
metricRegistry.counter(LabeledMetric.name("num_records").label("device_id", "1312").toString())
              .mark();
```

And if you have a metric with no label, you can call metric registry in its normal way:

```java
 metricRegistry.counter("num_records").mark();
```

But note that to make it work, you should also introduce the `LabelSupportedObjectNameFactory` (provided by this library)
when starting the JMX reporter:

```java
JmxReporter.forRegistry(metricRegistry)
           .createsObjectNamesWith(new LabelSupportedObjectNameFactory())
           .inDomain("my-metrics-domain")
           .build().start();
```
### Add it to your project

You can reference to this library by either of java build systems (Maven, Gradle, SBT or Leiningen) using snippets from this jitpack link:
[![](https://jitpack.io/v/sahabpardaz/label-supported-dropwizard-metrics.svg)](https://jitpack.io/#sahabpardaz/label-supported-dropwizard-metrics)
