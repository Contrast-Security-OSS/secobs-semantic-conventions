# Contrast Action Spans

<!-- toc -->

- [Definitions](#definitions)
- [Action Span Attributes](#action-span-attributes)
  * [Authentication Span](#authentication-span)
  * [Authorization Span](#authorization-span)

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

### Authentication Span

Used when span name is `authn-request`

<!-- semconv contrast.action.span.authn(full) -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `contrast.authentication.mechanism` | string | An authentication mechanism is a specific method or approach used to verify the identity of a user, system, or entity attempting to access a resource. | `password`; `token`; `biometric` | Recommended |
| `contrast.authentication.protocol` | string | An authentication protocol is a set of rules and procedures that dictate how authentication mechanisms should operate to establish trust and verify identities securely. | `oauth`; `saml`; `ldap`; `custom` | Recommended |

`contrast.authentication.mechanism` MUST be one of the following:

| Value  | Description |
|---|---|
| `password` | Users provide a username and password. |
| `certificate` | x509 certificate authentication or similar |
| `token` | Involves using a physical or virtual token to authenticate a user |
| `biometric` | file open or create action |
| `mfa` | Two or more of the above mechanisms are used |

`contrast.authentication.protocol` MUST be one of the following:

| Value  | Description |
|---|---|
| `saml` | Security Assertion Markup Language |
| `oauth` | Open Authentication and OIDC |
| `ldap` | Lightweight Directory Access Protocol |
| `kerberos` |  |
<!-- endsemconv -->

### Authorization Span

Used when span name is `authz-request`

<!-- semconv contrast.action.span.authz(full) -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `contrast.authorization.dac.permission` | string | Permission requested for access to the resource. The values here are very domain specific, but will always be normalized to a lowercase value in the data here. | `read`; `write`; `append`; `delete` | Recommended: If mechanism is 'dac' |
| `contrast.authorization.mac.labels` | string | Labels on the requested resource. The values here are very domain specific, but will always be normalized to a lowercase value in the data here. | `top_secret`; `confidential`; `internal`; `public` | Recommended: If mechanism is 'mac' |
| `contrast.authorization.mechanism` | string | How are authz decisions made for the resource. | `rbac`; `dac`; `pbac` | Recommended |
| `contrast.authorization.rbac.role` | string | Role Requested for authz check. The values here are very domain specific, but will always be normalized to a lowercase value in the data here. | `user`; `editor`; `manager` | Recommended: If mechanism is 'rbac' |

`contrast.authorization.mechanism` MUST be one of the following:

| Value  | Description |
|---|---|
| `rbac` | Role Based Access Control |
| `abac` | Attribute Based Access Control |
| `mac` | Mandatory Access Control (MAC) is a security model where access to resources is determined by the security labels assigned to subjects (users or processes) and objects (resources). |
| `dac` | Discretionary Access Control (DAC) is a model where owners of resources have the discretion to control access to their resources. |
| `pbac` | Policy Based Access Control |
| `hbac` | History Based Access Control |
| `tbac` | Time Based Access Control |
| `pbac` | Policy Based Access Control |
<!-- endsemconv -->
