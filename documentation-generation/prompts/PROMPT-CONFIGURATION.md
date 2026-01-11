# Prompt: Generate Configuration Documentation

> **Output:** `CONFIGURATION.md`

---

## The Prompt

````text
You are documenting the configuration requirements for a software project. 
First, detect the language/framework used, then analyze the codebase and write 
CONFIGURATION.md that explains everything needed to run this project.

## Before You Start

Create a notes file at `{ProjectName}.CONFIGURATION.notes.md` and build it
incrementally as you read each file. This protects against context limits.

**For each file that uses configuration:**

1. Read the file in its ENTIRETY - do not read partial line ranges
2. Immediately append any configuration findings to the notes file
3. Move to the next file

**Notes format:**

```
### Connection Strings / Database URLs
- Name: Purpose, example format

### App Settings / Config Values
- Key: Purpose, type, default, required?

### External Services
- Service name: Config keys needed, purpose

### Environment Variables
- VAR_NAME: Purpose, required in which environments

### Config Classes / Schemas
- ClassName: What settings it binds to
```

Start with config files (config.json, .env.example, settings.py, etc.), then 
search for configuration access patterns in code files.

If you cannot read a file completely, note that in the file entry.

After all files are processed, use the notes to write the final documentation.

## Writing the Documentation

Write for a developer who needs to:
- Set up the project locally for the first time
- Deploy to a new environment
- Troubleshoot configuration-related issues

Project: {ProjectName}

---

Structure your document roughly like this (adapt as needed):

# Configuration

## Overview
Brief context on how configuration works in this project.

## Required Settings

### Connection Strings / Database URLs
| Name | Purpose | Example |
|------|---------|---------|
| `DATABASE_URL` | Main database | `postgres://...` |

### Application Settings
| Setting | Purpose | Default | Required |
|---------|---------|---------|----------|
| `MAX_ITEMS` | Limit per request | 100 | No |

### External Services
| Service | Settings Needed | How to Get Credentials |
|---------|-----------------|------------------------|
| Stripe | `STRIPE_API_KEY` | Dashboard → API Keys |

## Environment Variables
| Variable | Purpose | Required In |
|----------|---------|-------------|
| `NODE_ENV` / `ENVIRONMENT` | Runtime env | All |
| `DB_PASSWORD` | Database auth | Production |

## Secrets
What secrets are needed and where they should be stored (vault, env vars, 
secrets manager, etc.). Never include actual values.

## Feature Flags
| Flag | What It Does | Default |
|------|--------------|---------|
| `ENABLE_BETA` | Shows new UI | false |

## Local Development Setup
Step-by-step to get running locally:
1. Copy `.env.example` to `.env`
2. Run database setup
3. etc.

## Environment-Specific Notes
Anything different about staging, production, etc.

---

## Files Analyzed

At the end of the document, include:

- **Fully read**: [list files you completely analyzed]
- **Partially read**: [list files that were too large to fully read]
- **Skipped**: [list any files not accessed, and why]
````

---

## Tips

- Check all config files: .env, config.json, settings.py, appsettings.json, etc.
- Look for config access patterns in code
- Environment variables often override config files in production
