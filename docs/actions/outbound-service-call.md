# Semantic Conventions for `outbound-service-call` Actions

Used when span name is `outbound-service-call`.

<!-- semconv contrast.action.span.outbound-service-call(full) -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `http.request.method` | string | HTTP request method. [1] | `POST`; `GET`; `DELETE` | Required |
| `http.response.status_code` | int | [HTTP response status code](https://datatracker.ietf.org/doc/html/rfc7231#section-6). |  | Conditionally Required: if and only if one was received. |
| `network.peer.address` | string | Peer address of the network connection - IP address or Unix domain socket name. | `10.1.2.80`; `/tmp/my.sock` | Recommended |
| `network.peer.port` | int | Peer port number of the network connection. | `80`; `8080`; `443` | Recommended: if `network.peer.address` populated |
| `network.protocol.version` | string | Version of the http protocol used. [2] | `1.0`; `1.1`; `2`; `3` | Recommended |
| `server.address` | string | Name of the remotely connected host. | `example.com`; `10.1.2.80`; `/tmp/my.sock` | Required |
| `server.port` | int | Port identifier of the [“URI origin”](https://www.rfc-editor.org/rfc/rfc9110.html#name-uri-origin) HTTP request is sent to. | `80`; `8080`; `443` | Required |

**[1]:** HTTP request method value SHOULD be “known” to the instrumentation. By default, this convention defines “known” methods as the ones listed in [RFC9110](https://www.rfc-editor.org/rfc/rfc9110.html#name-methods) and the PATCH method defined in [RFC5789](https://www.rfc-editor.org/rfc/rfc5789.html).

**[2]:** network.protocol.version refers to the version of the protocol used and might be different from the protocol client’s version. If the HTTP client has a version of 0.27.2, but sends HTTP version 1.1, this attribute should be set to 1.1.
<!-- endsemconv -->
