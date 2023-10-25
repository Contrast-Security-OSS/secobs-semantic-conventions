# metric.service.action.total
<!-- semconv metric.service.action.total(full) -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `contrast.action.type` | string | The type of action that was observed. | `file-open-create` | Required |
| `contrast.service.type` | string | The type of service this action was observed on. This value gives an indication of what other attributes will be part of this metric. | `http` | Required |

`contrast.action.type` MUST be one of the following:

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
| `authz-request` | Functions that perform authorization  actions |
| `el-execution` | Spring expression language execution |
| `ognl-execution` | Object-Graph Navigation Language expression execution. |

`contrast.service.type` MUST be one of the following:

| Value  | Description |
|---|---|
| `http` | http protocol type of service |
| `messaging` | messaging type of service |
| `rpc` | Remote Procedure Call type of service |
<!-- endsemconv -->