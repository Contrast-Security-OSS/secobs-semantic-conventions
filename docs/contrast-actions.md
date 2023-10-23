# metric.service.action.total
<!-- semconv metric.service.action.total(full) -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `contrast.action.type` | string | The type of action that was observed. | `file-open-create` | Required |
| `contrast.service.type` | string | The type of service this action was observed on. This value gives an indication of what other attributes will be part of this metric. | `http` | Required |

`contrast.action.type` MUST be one of the following:

| Value  | Description |
|---|---|
| `file-open-create` | file open or create action |
| `el-execution` | spring expression language execution |

`contrast.service.type` MUST be one of the following:

| Value  | Description |
|---|---|
| `http` | http protocol type of service |
| `messaging` | messaging type of service |
| `rpc` | Remote Procedure Call type of service |
<!-- endsemconv -->