# Semantic Conventions for `outbound-service-call` Actions

<!-- Re-generate TOC with `markdown-toc --no-first-h1 -i` -->

<!-- toc -->

- [outbound-service-call (http client) span duration](#outbound-service-call-http-client-span-duration)
- [HTTP request retries and redirects](#http-request-retries-and-redirects)

<!-- tocstop -->

Used when span name is `outbound-service-call`.

This span type represents an outbound HTTP request. There are two ways this can be achieved in an instrumentation:

1. Instrumentations SHOULD create an `outbound-service-call` span for each attempt to send an HTTP request over the wire.
   In case the request is resent, the resend attempts MUST follow the [HTTP resend spec](#http-request-retries-and-redirects).
   In this case, instrumentations SHOULD NOT (also) emit a logical encompassing `outbound-service-call` span.

2. If for some reason it is not possible to emit a span for each send attempt (because e.g. the instrumented library does not expose hooks that would allow this),
   instrumentations MAY create an `outbound-service-call` span for the top-most operation of the HTTP client.
   In this case, the `url.full` MUST be the absolute URL that was originally requested, before any HTTP-redirects that may happen when executing the request.

<!-- semconv contrast.action.span.outbound-service-call(full) -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `http.request.method` | string | HTTP request method. [1] | `POST`; `GET`; `DELETE` | Required |
| `http.response.status_code` | int | [HTTP response status code](https://datatracker.ietf.org/doc/html/rfc7231#section-6). |  | Conditionally Required: if and only if one was received. |
| `network.peer.address` | string | Peer address of the network connection - IP address or Unix domain socket name. | `10.1.2.80`; `/tmp/my.sock` | Recommended |
| `network.peer.port` | int | Peer port number of the network connection. | `80`; `8080`; `443` | Recommended: if `network.peer.address` populated |
| `network.protocol.version` | string | Version of the http protocol used. [2] | `1.0`; `1.1`; `2`; `3` | Recommended |
| `server.address` | string | Name of the remotely connected host. [3] | `example.com`; `10.1.2.80`; `/tmp/my.sock` | Required |
| `server.port` | int | Port identifier of the [“URI origin”](https://www.rfc-editor.org/rfc/rfc9110.html#name-uri-origin) HTTP request is sent to. [4] | `80`; `8080`; `443` | Required |
| `url.full` | string | Absolute URL describing a network resource according to [RFC3986](https://www.rfc-editor.org/rfc/rfc3986) [5] | `https://www.foo.bar/search?q=OpenTelemetry#SemConv`; `//localhost` | Required |

**[1]:** HTTP request method value SHOULD be “known” to the instrumentation. By default, this convention defines “known” methods as the ones listed in [RFC9110](https://www.rfc-editor.org/rfc/rfc9110.html#name-methods) and the PATCH method defined in [RFC5789](https://www.rfc-editor.org/rfc/rfc5789.html).

**[2]:** network.protocol.version refers to the version of the protocol used and might be different from the protocol client’s version. If the HTTP client has a version of 0.27.2, but sends HTTP version 1.1, this attribute should be set to 1.1.

**[3]:** If an HTTP client request is explicitly made to an IP address, e.g. `http://x.x.x.x:8080`, then server.address SHOULD be the IP address x.x.x.x. A DNS lookup SHOULD NOT be used.

**[4]:** When observed from the client side, and when communicating through an intermediary, `server.port`` SHOULD represent the server port behind any intermediaries, for example proxies, if it’s available.

**[5]:** For network calls, URL usually has `scheme://host[:port][path][?query][#fragment]` format, where the fragment is not transmitted over HTTP, but if it is known, it SHOULD be included nevertheless. `url.full` MUST NOT contain credentials passed via URL in form of `https://username:password@www.example.com/`. In such case username and password SHOULD be redacted and attribute’s value SHOULD be `https://REDACTED:REDACTED@www.example.com/`. `url.full` SHOULD capture the absolute URL when it is available (or can be reconstructed) and SHOULD NOT be validated or modified except for sanitizing purposes.
<!-- endsemconv -->

## outbound-service-call (http client) span duration

There are some minimal constraints that SHOULD be honored:

* `outbound-service-call` spans SHOULD start sometime before the first request byte is sent. This may or may not include connection time.
* `outbound-service-call` spans SHOULD end sometime after the HTTP response headers are fully read (or when they fail to be read). This may or may not include reading the response body.

If there is any possibility for application code to not fully read the HTTP response
(and for the HTTP client library to then have to clean up the HTTP response asynchronously),
the HTTP client span SHOULD NOT be ended in this cleanup phase,
and instead SHOULD end at some point after the HTTP response headers are fully read (or fail to be read).
This avoids the span being ended asynchronously later on at a time
which is no longer directly associated with the application code which made the HTTP request.

Because of the potential for confusion around this, HTTP client library instrumentations SHOULD document their behavior around ending HTTP client spans.

## HTTP request retries and redirects

Retries and redirects cause more than one physical HTTP request to be sent.
A request is resent when an HTTP client library sends more than one HTTP request to satisfy the same API call.
This may happen due to following redirects, authorization challenges, 503 Server Unavailable, network issues, or any other.

Each time an HTTP request is resent, the `http.resend_count` attribute SHOULD be added to each repeated span and set to the ordinal number of the request resend attempt.
