# http.server.action.total
<!-- semconv metric.http.server.action.total(full) -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `action` | string | The type of action that was observed. | `file-open-create` | Required |
| `http.method` | string | http method used when the action was encountered. | `['GET', 'POST']` | Required |
| `http.route` | string | http route used when the action was encountered. | `/foo/bar` | Required |

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
| `authz-request` | Functions that perform authorization  actions |
| `el-execution` | Spring expression language execution |
| `ognl-execution` | Object-Graph Navigation Language expression execution. |
<!-- endsemconv -->