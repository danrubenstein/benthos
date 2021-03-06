Tracer Types
============

This document was generated with `benthos --list-tracers`

A tracer type represents a destination for Benthos to send opentracing events to
such as Jaeger.

When a tracer is configured all messages will be allocated a root span during
ingestion that represents their journey through a Benthos pipeline. Many Benthos
processors create spans, and so opentracing is a great way to analyse the
pathways of individual messages as they progress through a Benthos instance.

Some inputs, such as `http_server` and `http_client`, are capable of
extracting a root span from the source of the message (HTTP headers). This is
a work in progress and should eventually expand so that all inputs have a way of
doing so.

A tracer config section looks like this:

``` yaml
tracer:
  type: foo
  foo:
    bar: baz
```

WARNING: Although the configuration spec of this component is stable the format
of spans, tags and logs created by Benthos is subject to change as it is tuned
for improvement.

## `jaeger`

``` yaml
type: jaeger
jaeger:
  agent_address: localhost:6831
  flush_interval: ""
  sampler_manager_address: ""
  sampler_param: 1
  sampler_type: const
  service_name: benthos
  tags: {}
```

Send spans to a Jaeger agent.

Available sampler types are: const, probabilistic, ratelimiting and remote.

## `none`

``` yaml
type: none
none: {}
```

Do not send opentracing events anywhere.
