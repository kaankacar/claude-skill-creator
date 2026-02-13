# YAML Frontmatter Specification

## Required Fields

```yaml
---
name: skill-name-in-kebab-case
description: What it does and when to use it. Include specific trigger phrases.
---
```

## All Optional Fields

```yaml
name: skill-name
description: [required description]
license: MIT
allowed-tools: "Bash(python:*) Bash(npm:*) WebFetch"
compatibility: "Requires Node.js 18+"
metadata:
  author: Company Name
  version: 1.0.0
  mcp-server: server-name
  category: productivity
  tags: [project-management, automation]
  documentation: https://example.com/docs
  support: support@example.com
```

## Field Rules

### name
- kebab-case only
- No spaces or capitals
- Must match folder name
- Cannot start with "claude" or "anthropic"

### description
- MUST include what it does AND when to use it
- Under 1024 characters
- No XML angle brackets (< or >)
- Include specific trigger phrases users would say
- Include negative triggers if scope could be confused

### license
- Use standard SPDX identifiers: MIT, Apache-2.0, etc.

### allowed-tools
- Space-separated list of tool patterns
- Restricts which tools the skill can invoke

### compatibility
- 1-500 characters
- Describe environment requirements

### metadata
- Any custom key-value pairs
- Suggested: author, version, mcp-server

## Security Restrictions

**Forbidden in frontmatter:**
- XML angle brackets (< >)
- Skills with "claude" or "anthropic" in name
- Code execution in YAML values

**Allowed:**
- Standard YAML types (strings, numbers, booleans, lists, objects)
- Custom metadata fields
- Long descriptions (up to 1024 characters)
