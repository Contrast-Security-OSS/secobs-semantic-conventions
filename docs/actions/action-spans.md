# Messaging Systems


## Definitions

The span name SHOULD be set to the action name:

```
<action name>
```

## Action Span Attrinbutes

<!-- semconv contrast.action.span.authn(full) -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `authentication.mechanism` | string | An authentication mechanism is a specific method or approach used to verify the identity of a user, system, or entity attempting to access a resource. | `password`; `token`; `biometric` | Recommended |
| `authentication.protocol` | string | An authentication protocol is a set of rules and procedures that dictate how authentication mechanisms should operate to establish trust and verify identities securely. | `oauth`; `saml`; `ldap`; `custom` | Recommended |

`authentication.mechanism` MUST be one of the following:

| Value  | Description |
|---|---|
| `password` | Users provide a username and password. |
| `certificate` | x509 certificate authentication or similar |
| `token` | Involves using a physical or virtual token to authenticate a user |
| `biometric` | file open or create action |
| `mfa` | Two or more of the above mechanisms are used |

`authentication.protocol` MUST be one of the following:

| Value  | Description |
|---|---|
| `saml` | Security Assertion Markup Language |
| `oauth` | Open Authentication and OIDC |
| `ldap` | Lightweight Directory Access Protocol |
| `kerberos` |  |
| `custom` | A custom implementation is being used and the protocol cannot be determined |
<!-- endsemconv -->