# OwnBackup — Naming Convention Reference

## Format

```
[Organisation Name] - [Environment] - [Org Name or ID] - [Type: Data or Metadata]
```

## Field definitions

| Field | Description | Example |
|---|---|---|
| Organisation Name | The name of the Salesforce customer org | Acme Corp |
| Environment | The Salesforce environment type | Production / Sandbox |
| Org Name or ID | The Salesforce Org ID or sandbox name | 00D000000000001 / DevSandbox |
| Type | The content type being backed up | Data / Metadata |

## Examples

```
Acme Corp - Production - 00D000000000001 - Data
Acme Corp - Production - 00D000000000001 - Metadata
Acme Corp - Sandbox - DevSandbox - Data
Acme Corp - Sandbox - DevSandbox - Metadata
```

## Rules

- Always use hyphens ( - ) as separators, never underscores or slashes
- Capitalise the first letter of each field value
- Use the full Org ID for production environments
- Use the sandbox name (not ID) for sandbox environments
- Always create both a Data and Metadata service for each environment
