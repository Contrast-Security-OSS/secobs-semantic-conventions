# Security Observability Semantic Conventions

The Semantic Conventions define a common set of (semantic) attributes which
provide meaning to data when collecting, producing and consuming it.
The Semantic Conventions specify among other things span names and kind, metric
instruments and units as well as attribute names, types, meaning and valid
values. For a detailed definition of the Semantic Conventions' scope see
[Semantic Conventions Stability](https://opentelemetry.io/docs/specs/otel/versioning-and-stability/#semantic-conventions-stability).
The benefit to using Semantic Conventions is in following a common naming
scheme that can be standardized across a codebase, libraries, and platforms.
This allows easier correlation and consumption of data.

Contrast standardizes on otel metrics and extend from them. See
[OTel Semantic Conventions](https://github.com/open-telemetry/semantic-conventions/tree/v1.22.0/docs)
for a foundational understanding of what we build on top of.

Semantic Conventions by signals:

- [Resource](resource/README.md): Semantic Conventions for resources.
- [Trace](general/trace.md): Semantic Conventions for traces and spans.
- [Metrics](general/metrics.md): Semantic Conventions for metrics.
