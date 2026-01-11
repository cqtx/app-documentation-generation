# Project Documentation Generator

Generate natural, human-readable documentation for existing software projects by
reverse-engineering what *should* have been written during development.

## Philosophy

Instead of creating AI-specific documentation formats, we generate standard
documentation that any developer (or AI) already knows how to read:

- `ARCHITECTURE.md` - How the system is built and why
- `DATA.md` - Entities, relationships, database schema
- `WORKFLOWS.md` - Key business processes end-to-end
- `API.md` - Endpoints, contracts, authentication
- `CONFIGURATION.md` - Settings, environment variables, secrets

## Quick Start

### For a Single Project

Run these prompts in order (skip any that don't apply):

1. `PROMPT-ARCHITECTURE.md` → Creates `ARCHITECTURE.md`
2. `PROMPT-DATA.md` → Creates `DATA.md`
3. `PROMPT-WORKFLOWS.md` → Creates `WORKFLOWS.md`
4. `PROMPT-API.md` → Creates `API.md`
5. `PROMPT-CONFIGURATION.md` → Creates `CONFIGURATION.md`

### For a Multi-Project Repository

1. Document each project using the prompts above
2. Run `PROMPT-SOLUTION.md` at the repo root → Creates `SOLUTION.md`

## Which Prompts to Run

Not every project needs every document. Use this guide:

| Prompt                     | When to Use                                    |
| -------------------------- | ---------------------------------------------- |
| `PROMPT-ARCHITECTURE.md`   | **Always** - every project                     |
| `PROMPT-DATA.md`           | Has entities, database access, or manages data |
| `PROMPT-WORKFLOWS.md`      | Has business logic or processes                |
| `PROMPT-API.md`            | Web API, REST endpoints, or HTTP interface     |
| `PROMPT-CONFIGURATION.md`  | **Always** - every project needs setup info    |
| `PROMPT-SOLUTION.md`       | Multi-project repositories only                |

### Examples by Project Type

| Project Type                | Prompts to Run                          |
| --------------------------- | --------------------------------------- |
| Web API / Backend Service   | All                                     |
| Library (business logic)    | ARCHITECTURE, DATA, WORKFLOWS, CONFIG   |
| Library (utilities/helpers) | ARCHITECTURE, CONFIGURATION             |
| Worker / Background Service | ARCHITECTURE, DATA, WORKFLOWS, CONFIG   |
| Shared / Common Package     | ARCHITECTURE, CONFIGURATION             |
| CLI Tool                    | ARCHITECTURE, CONFIGURATION             |
| Frontend App                | ARCHITECTURE, WORKFLOWS, CONFIGURATION  |

## How to Use the Prompts

1. Open a prompt file
2. Copy the prompt text
3. Replace `{ProjectName}` with your actual project name
4. Give the AI access to your codebase
5. Save the output as the corresponding `.md` file in your project

## Generated Documentation Structure

```text
Repository Root/
├── SOLUTION.md              ← Repository overview (for multi-project)
│
├── api-service/
│   ├── ARCHITECTURE.md      ← System design
│   ├── DATA.md              ← Entities and schema
│   ├── WORKFLOWS.md         ← Business processes
│   ├── API.md               ← Endpoints (if applicable)
│   └── CONFIGURATION.md     ← Settings required
│
├── core-library/
│   ├── ARCHITECTURE.md
│   └── ...
│
└── shared/
    └── ARCHITECTURE.md      ← Even simple libraries benefit
```

## Using for Troubleshooting

Once generated, this documentation helps AI understand your codebase when
debugging issues.

**Which documents to provide based on the problem:**

| Issue Type                     | Provide These Documents        |
| ------------------------------ | ------------------------------ |
| Understanding a component      | ARCHITECTURE.md                |
| Database or entity errors      | ARCHITECTURE.md + DATA.md      |
| Process not working correctly  | ARCHITECTURE.md + WORKFLOWS.md |
| Configuration/deployment issue | CONFIGURATION.md               |
| API integration problem        | API.md + WORKFLOWS.md          |
| Cross-project issue            | SOLUTION.md + relevant project docs |

**How to ask for help:**

1. Start with the relevant documentation files
2. Describe the error or unexpected behavior
3. Include code snippets if helpful

The AI already understands the system from the documentation - it knows the
components, data model, and workflows. This lets it give targeted answers
instead of generic troubleshooting steps.

## Maintenance

Regenerate documentation when:

- Major architectural changes occur
- New entities or workflows are added
- API contracts change significantly

Small changes can often be manually edited - these are meant to be living
documents, not generated artifacts.
