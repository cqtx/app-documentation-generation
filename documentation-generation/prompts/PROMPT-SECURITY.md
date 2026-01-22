# Prompt: Generate Security Documentation

> **Output:** `SECURITY.md`
> **Use for:** Projects handling authentication, sensitive data, or external integrations

---

## The Prompt

````text
You are documenting the security considerations for a software project. First,
detect the language/framework used, then analyze the codebase and write
SECURITY.md that explains how security is handled and what developers need
to know to maintain it.

## Before You Start

Create a notes file at `../output/_notes/{ProjectName}/SECURITY.notes.md` and
build it incrementally as you read each file. This protects against context limits.

**For each file that handles security concerns:**

1. Read files completely. For files over 500 lines, read in chunks and append findings to the notes file as you go
2. Immediately append security-relevant findings to the notes file
3. Move to the next file

**Notes format:**

```
### Authentication
- Method used (JWT, sessions, OAuth, API keys)
- Where tokens/credentials are validated
- Token expiration and refresh handling

### Authorization
- How permissions are checked
- Role/permission model
- Where access control is enforced

### Data Protection
- Sensitive fields identified
- Encryption at rest/in transit
- PII handling

### Input Validation
- Where validation occurs
- Sanitization patterns used
- Known gaps or concerns

### External Integrations
- Third-party services called
- How credentials are stored
- Data shared externally

### Potential Concerns
- Patterns that look risky
- Missing validations
- Areas needing review
```

Look for: auth middleware, login handlers, permission checks, encryption utilities,
input validation, sanitization functions, and security-related configuration.

If you cannot read a file completely, note that in the file entry.

After all files are processed, use the notes to write the final documentation.

## Writing the Documentation

Write for a developer who needs to:
- Understand how authentication and authorization work
- Maintain security without introducing vulnerabilities
- Know what to audit or test when making changes

Be factual about what exists. Note gaps or concerns without being alarmist.

Project: {ProjectName}

---

Structure your document roughly like this (adapt as needed):

# Security

## Overview
Brief summary of the security model. What's protected and how?

## Authentication

### How Users Authenticate
Login flow, token format, where credentials are verified.

### Session/Token Management
How sessions or tokens are created, stored, validated, and expired.
Where to look if auth is broken.

### Password Handling
How passwords are hashed/stored (if applicable). Password reset flow.

## Authorization

### Permission Model
Roles, permissions, or access levels used. How they're assigned.

### Where Access is Checked
Middleware, decorators, or checks that enforce permissions.
What happens when access is denied.

### Resource-Level Access
How ownership or resource-specific access is determined.

## Data Protection

### Sensitive Data
What data is considered sensitive. How it's identified in the code.

### Encryption
What's encrypted, how, and where keys are managed.

### Data Retention
How long data is kept. Deletion or anonymization processes.

## Input Handling

### Validation
Where and how input is validated. Common patterns used.

### Known Risks
Any areas where validation is weak or missing. SQL injection, XSS,
or other OWASP concerns to watch for.

## External Integrations

### Third-Party Services
What external services are called. What data is sent to them.

### Credential Storage
How API keys and secrets for external services are managed.

## Security Checklist for Changes

When modifying this project, verify:
- [ ] New endpoints have appropriate auth checks
- [ ] User input is validated before use
- [ ] Sensitive data isn't logged or exposed in errors
- [ ] New dependencies don't introduce vulnerabilities

## Known Limitations

Honest assessment of security gaps or areas needing improvement.

---

## Files Analyzed

At the end of the document, include:

- **Fully read**: Files you read completely in one pass
- **Partially read**: Files read in chunks due to size (note approximate line count)
- **Skipped**: Files not read, with reason (binary, minified, generated, too large, etc.)
````

---

## Tips

- Focus on auth handlers, middleware, and security-related utilities
- Check for common vulnerabilities: SQL injection, XSS, CSRF, insecure deserialization
- Note both what's done well and what's missing
- Don't include actual secrets or credentials in the documentation
