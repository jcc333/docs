## The analytics pipeline

This section illustrates how to use the analytics pipeline to extract insight from
your raw sensor data.


### Pipeline overview

A pipeline defines a sequence of operations that are applied to a stream of data
from a sensor, resulting in a new output stream of data points.
Pipeline operations are typically mathematical functions, such as applying a scale factor or
averaging over a period of time.

Pipelines operate individually on each sensor in a selector. Therefore, for a basic
pipeline, there's a one-to-one correspondence between input sensor streams and
output streams.
Combining streams across several sensors or devices is covered in the next section.

`[ diagram of where a basic pipeline fits in a read query ]`

TempoIQ supports many pipeline operations as part of the client libraries.
See the Analytics API reference for details.


### Using pipelines in a read query

Analyzing historical sensor data with a pipeline is straightforward: simply
supply a pipeline object as an argument in the `read` call.

#### Example

Thermostat devices record data once a minute, but it is unnecessary to have this
level of granularity in a week-long graph. You can use the rollup pipeline operation
to downsample the raw data streams to hourly averages:

```
pipe = Pipeline.start().rollup("1hour", "mean");

response = client.read(sensors, pipe, start, end);
```

### Chaining pipeline operations

An analytics pipeline can contain several operations in sequence. Each operation takes
the result of the previous operation as its input. This enables you to compose complex
analysis functions out of simple component operations. See the pipeline cookbook for
example pipelines that are composed from the basic pipeline operations.