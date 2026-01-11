# Prompt: Generate API Documentation

> **Output:** `API.md`
> **Use for:** Web API projects, services with HTTP endpoints

---

## The Prompt

````text
You are documenting the API for a web project. First, detect the language and 
framework used, then analyze the codebase and write API.md that explains the 
available endpoints, how to use them, and what to expect.

## Before You Start

Create a notes file at `_notes/{ProjectName}.API.notes.md` and build it
incrementally as you read each file. This protects against context limits.

**For each route handler/controller file in the project:**

1. Read the file in its ENTIRETY - do not read partial line ranges
2. Immediately append notes for that handler to `_notes/{ProjectName}.API.notes.md`
3. Move to the next file

**Notes format for each route handler:**

```
### HandlerName / ControllerName
- **Route base**: Base path/prefix
- **Auth**: Authentication requirements

#### GET /endpoint
- **Purpose**: One sentence
- **Parameters**: Query/route params with types
- **Returns**: Response type
- **Auth**: If different from base level

(Repeat for each endpoint)
```

If you cannot read a file completely, note that in the file entry.

After all files are processed, use the notes to write the final documentation.

## Writing the Documentation

Write for a developer who needs to:
- Call this API from another service or frontend
- Understand what's available and how to authenticate
- Debug integration issues

Project: {ProjectName}

---

Structure your document roughly like this (adapt as needed):

# API Documentation

## Overview
What does this API do? Who are the intended consumers?

## Base URL
Where is this hosted? Any environment-specific URLs?

## Authentication
How do callers authenticate? JWT, API keys, cookies, OAuth? 
What headers are required?
How to get credentials?

## Common Patterns
- How errors are returned (problem details, custom format?)
- Pagination approach
- Rate limiting if any
- Versioning scheme

## Endpoints

### [Group Name]

#### `GET /api/resource`
What it does.

**Parameters:**
- `param1` (query, required) - Description

**Response:** `200 OK`
```json
{
  "example": "response"
}
```

**Errors:**
- `401` - Not authenticated
- `404` - Resource not found

(Repeat for each endpoint)

## Webhooks / Events
If the API publishes events or calls webhooks, document them here.

## Examples
Common usage patterns. How to create a resource then fetch it, etc.

---

## Files Analyzed

At the end of the document, include:

- **Fully read**: [list files you completely analyzed]
- **Partially read**: [list files that were too large to fully read]
- **Skipped**: [list any files not accessed, and why]
````

---

## Tips

- Route definitions and handlers are the source of truth
- Include realistic example payloads
- Document error responses - they're what people need when debugging
