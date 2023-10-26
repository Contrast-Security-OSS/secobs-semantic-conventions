# Semantic Conventions for Contrast Actions

Actions are a concept for Security Observability. They are modeled as a metric
so that actions are seen for every requests and collected in a scalable
manner for the agent. We will never miss an action on a particular execution path.
The data used in the action is captured as attributes within a span. Since
capturing and processing spans is considered an expensive activity, this data is captured
as part of a sampling activity.

<!-- toc -->

- [Http Actions](#http-actions)
  - [Metric: `http.server.action.total`](#metric-httpserveractiontotal)

<!-- tocstop -->

## Http Actions

### Metric: `http.server.action.total`

<!-- semconv metric.http.server.action.total(full) -->

| Attribute     | Type   | Description                                       | Examples                            | Requirement Level |
| ------------- | ------ | ------------------------------------------------- | ----------------------------------- | ----------------- |
| `action`      | string | The type of action that was observed.             | `file-open-create`; `authn-request` | Required          |
| `http.method` | string | http method used when the action was encountered. | `GET`; `POST`                       | Required          |
| `http.route`  | string | http route used when the action was encountered.  | `/foo/bar`                          | Required          |

`action` MUST be one of the following:

| Value                   | Description                                                          |
| ----------------------- | -------------------------------------------------------------------- |
| `storage-query`         | Functions that execute queries                                       |
| `file-open-create`      | file open or create action                                           |
| `url-forward`           | Any function designed to forward a request to another URL            |
| `url-redirect`          | Function that result in an http 302 redirect code sent to the client |
| `host-cmd-exec`         | system shell command execution                                       |
| `ldap-query`            | Functions that result in and ldap query operation                    |
| `smtp-exec`             | Functions that result in an SMTP command execution                   |
| `outbound-service-call` | Functions that result in external calls to other services            |
| `authn-request`         | Functions that perform authentication actions                        |
| `authz-request`         | Functions that perform authorization actions                         |
| `el-execution`          | Spring expression language execution                                 |
| `ognl-execution`        | Object-Graph Navigation Language expression execution.               |

<!-- endsemconv -->
