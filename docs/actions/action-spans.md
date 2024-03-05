# Contrast Action Spans

<!-- toc -->

- [Definitions](#definitions)
- [Action Span Attributes](#action-span-attributes)
  * [Java Specific action types](#java-specific-action-types)

<!-- tocstop -->

## Definitions

The span name MUST be set to the action name:

```
<action name>
```

Valid action names are are listed in the action attribute for metrics:

<!-- semconv attributes.contrast.actions(full) -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `action` | string | The type of action that was observed. | `file-open-create`; `authn-request` | Required |

`action` MUST be one of the following:

| Value  | Description |
|---|---|
| `storage-query` | Functions that execute queries |
| `file-open-create` | file open or create action |
| `url-forward` | Any function designed to forward a request to another URL |
| `url-redirect` | Function that result in an http 302 redirect code sent to the client |
| `host-cmd-exec` | system shell command execution |
| `ldap-query` | Functions that result in and ldap query operation |
| `smtp-exec` | Functions that result in an SMTP command execution |
| `outbound-service-call` | Functions that result in external calls to other services |
| `authn-request` | Functions that perform authentication actions |
| `authz-request` | Functions that perform authorization actions |
| `el-execution` | Spring expression language execution |
| `ognl-execution` | Object-Graph Navigation Language expression execution. |
<!-- endsemconv -->

## Action Span Attributes

Each Action Span has attributes that describe the action observed. For instance, an `authn-request` span
will list the authentication mechanism along with other authentication-related attributes
An action span for the `storage-query` action will have a different set of attributes
targeted toward describing that action.

* [authn-request](authn-request.md)
* [authz-request](authz-request.md)
* [storage-query](storage-query.md)
* [file-open-create](file-open-create.md)
* [outbound-service-call](outbound-service-call.md)
* [url-forward](url-forward.md)
* [url-redirect](url-redirect.md)
* [host-cmd-exec](host-cmd-exec.md)
* [ldap-query](ldap-query.md)
* [smtp-exec](smtp-exec.md)

### Java Specific action types

* [el-execution](el-execution.md)
* [ognl-execution](ognl-execution.md)
