# Semantic Conventions for `security-control` Actions

Used when span name is `security-control`.

<!-- semconv contrast.action.span.security-control(full) -->
| Attribute  | Type | Description  | Examples  | Requirement Level |
|---|---|---|---|---|
| `method` | string | The method of the custom security control. | `com.Acme.OldSecurity.DoLegacySecurity` | Required |
| `name` | string | The name of the custom security control. | `My Custom Security Control` | Recommended |
| `rules` | string | The rules applicable to the custom security control. | `reflected-xss; path-traversal` | Recommended |
| `type` | string | The custom security control type. | `sanitizer; input-validator` | Recommended |

`type` MUST be one of the following:

| Value  | Description |
|---|---|
| `sanitizer` | Sanitizer |
| `input-validator` | Input Validator |
| `regex-validator` | Regex Validator |
<!-- endsemconv -->
