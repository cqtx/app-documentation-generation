# Prompt: Generate Dependencies Documentation

> **Output:** `DEPENDENCIES.md`
> **Use for:** Projects with significant external dependencies or compliance requirements

---

## The Prompt

````text
You are documenting the dependencies for a software project. First, detect the
language/framework and package manager used, then analyze the dependency files
and write DEPENDENCIES.md that explains what the project depends on and why.

## Before You Start

Create a notes file at `../output/_notes/{ProjectName}/DEPENDENCIES.notes.md` and
build it incrementally as you read each file. This protects against context limits.

**For each dependency manifest file:**

1. Read files completely. For files over 500 lines, read in chunks and append findings to the notes file as you go
2. Categorize each dependency and note its purpose
3. Move to the next file

**Notes format:**

```
### Runtime Dependencies
- package-name: version, purpose, why chosen

### Development Dependencies
- package-name: version, purpose (testing, build, lint, etc.)

### Framework/Platform
- Core framework and version
- Runtime requirements

### Notable Choices
- Packages where alternatives exist and why this one was chosen

### Concerns
- Outdated packages
- Packages with known issues
- Packages that may need replacement
```

Check: package.json, requirements.txt, Gemfile, pom.xml, build.gradle,
Cargo.toml, go.mod, *.csproj, and similar dependency files.

If you cannot read a file completely, note that in the file entry.

After all files are processed, use the notes to write the final documentation.

## Writing the Documentation

Write for a developer who needs to:
- Understand why specific packages were chosen
- Evaluate whether to update or replace dependencies
- Assess licensing implications
- Onboard quickly without researching each package

Project: {ProjectName}

---

Structure your document roughly like this (adapt as needed):

# Dependencies

## Overview
Package manager(s) used. General approach to dependency management.

## Runtime Dependencies

### Core Framework
| Package | Version | Purpose |
|---------|---------|---------|
| express | 4.18.x | Web framework |

Why this framework was chosen. Key features used.

### Database
| Package | Version | Purpose |
|---------|---------|---------|
| pg | 8.x | PostgreSQL client |

Database driver and any ORM/query builder.

### Authentication
| Package | Version | Purpose |
|---------|---------|---------|
| passport | 0.6.x | Auth middleware |

Auth-related packages and how they're used.

### Utilities
| Package | Version | Purpose |
|---------|---------|---------|
| lodash | 4.x | Utility functions |
| dayjs | 1.x | Date handling |

Common utility packages. Note if only partially used.

### External Services
| Package | Version | Purpose |
|---------|---------|---------|
| stripe | 12.x | Payment processing |
| aws-sdk | 3.x | AWS integrations |

SDKs for third-party services.

## Development Dependencies

### Testing
| Package | Version | Purpose |
|---------|---------|---------|
| jest | 29.x | Test runner |
| supertest | 6.x | HTTP testing |

### Build Tools
| Package | Version | Purpose |
|---------|---------|---------|
| typescript | 5.x | Type checking |
| esbuild | 0.19.x | Bundling |

### Code Quality
| Package | Version | Purpose |
|---------|---------|---------|
| eslint | 8.x | Linting |
| prettier | 3.x | Formatting |

## Licenses

| License Type | Packages |
|--------------|----------|
| MIT | express, lodash, ... |
| Apache 2.0 | ... |
| Other | ... (note any concerns) |

Any licensing considerations for commercial use or distribution.

## Update Policy

How dependencies should be updated:
- Security patches: immediately
- Minor versions: monthly review
- Major versions: evaluate breaking changes

Any packages pinned to specific versions and why.

## Known Issues

Packages with known problems, deprecation warnings, or planned replacements.

## Alternatives Considered

For key packages, note alternatives that were evaluated and why they weren't chosen.
This helps future developers understand the decision context.

---

## Files Analyzed

At the end of the document, include:

- **Fully read**: Files you read completely in one pass
- **Partially read**: Files read in chunks due to size (note approximate line count)
- **Skipped**: Files not read, with reason (binary, minified, generated, too large, etc.)
````

---

## Tips

- Focus on explaining *why* packages were chosen, not just listing them
- Group related packages together (all testing, all database, etc.)
- Note packages that are outdated or have security advisories
- Include license information for compliance-sensitive projects
