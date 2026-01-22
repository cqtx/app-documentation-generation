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
- `SECURITY.md` - Authentication, authorization, data protection (optional)
- `DEPENDENCIES.md` - Package inventory with licenses and rationale (optional)

## Quick Start

### For a Single Project

Run these prompts in order (skip any that don't apply):

1. `PROMPT-ARCHITECTURE.md` → Creates `ARCHITECTURE.md`
2. `PROMPT-DATA.md` → Creates `DATA.md`
3. `PROMPT-WORKFLOWS.md` → Creates `WORKFLOWS.md`
4. `PROMPT-API.md` → Creates `API.md`
5. `PROMPT-CONFIGURATION.md` → Creates `CONFIGURATION.md`
6. `PROMPT-SECURITY.md` → Creates `SECURITY.md` (optional)
7. `PROMPT-DEPENDENCIES.md` → Creates `DEPENDENCIES.md` (optional)

### For a Multi-Project Repository

1. Document each project using the prompts above
2. Run `PROMPT-REPOSITORY.md` at the repo root → Creates `REPOSITORY.md`

## Which Prompts to Run

Not every project needs every document. Use this guide:

| Prompt                    | When to Use                                       |
| ------------------------- | ------------------------------------------------- |
| `PROMPT-ARCHITECTURE.md`  | **Always** - every project                        |
| `PROMPT-DATA.md`          | Has entities, database access, or manages data    |
| `PROMPT-WORKFLOWS.md`     | Has business logic or processes                   |
| `PROMPT-API.md`           | Web API, REST endpoints, or HTTP interface        |
| `PROMPT-CONFIGURATION.md` | **Always** - every project needs setup info       |
| `PROMPT-SECURITY.md`      | Handles auth, sensitive data, or compliance needs |
| `PROMPT-DEPENDENCIES.md`  | Significant dependencies or license requirements  |
| `PROMPT-REPOSITORY.md`    | Multi-project repositories only                   |

### Examples by Project Type

| Project Type                | Prompts to Run                                  |
| --------------------------- | ----------------------------------------------- |
| Web API / Backend Service   | All (including SECURITY, DEPENDENCIES)          |
| Library (business logic)    | ARCHITECTURE, DATA, WORKFLOWS, CONFIG           |
| Library (utilities/helpers) | ARCHITECTURE, CONFIGURATION, DEPENDENCIES       |
| Worker / Background Service | ARCHITECTURE, DATA, WORKFLOWS, CONFIG           |
| Shared / Common Package     | ARCHITECTURE, CONFIGURATION                     |
| CLI Tool                    | ARCHITECTURE, CONFIGURATION                     |
| Frontend App                | ARCHITECTURE, WORKFLOWS, CONFIG, SECURITY       |

## Output Locations

Within this workspace, all generated files are saved to:

```text
documentation-generation/
├── output/
│   ├── {ProjectName}/           # Generated documentation
│   │   ├── ARCHITECTURE.md
│   │   ├── DATA.md
│   │   └── ...
│   └── _notes/                  # Working notes
│       └── {ProjectName}/
│           ├── ARCHITECTURE.notes.md
│           ├── DATA.notes.md
│           └── ...
```

The `_notes/` folder contains incremental notes created while analyzing files.
These protect against context limits.

## Using for Troubleshooting

When helping with questions or debugging issues, navigate the generated
documentation to understand the codebase.

### Navigation Path

Follow this path from general to specific:

1. **REPOSITORY.md** (if multi-project) → Identifies which project(s) are involved
2. **ARCHITECTURE.md** → Provides the component map for that project
3. **Specific doc** → Based on the issue type (see table below)
4. **Source code** → Only if documentation doesn't fully answer the question

Load 2-3 focused documents instead of everything to keep context clear.

### Which Document for Which Problem

| Issue Type                          | Navigation Path                   |
| ----------------------------------- | --------------------------------- |
| Understanding a component           | ARCHITECTURE.md                   |
| Database or entity errors           | ARCHITECTURE.md → DATA.md         |
| Process not working correctly       | ARCHITECTURE.md → WORKFLOWS.md    |
| API call failing, wrong response    | ARCHITECTURE.md → API.md          |
| Configuration/deployment issue      | CONFIGURATION.md                  |
| Authentication/authorization        | ARCHITECTURE.md → SECURITY.md     |
| Dependency conflicts/updates        | DEPENDENCIES.md                   |
| Cross-project issue                 | REPOSITORY.md → relevant projects |

### Responding to Help Requests

When the user describes a problem:

1. Identify keywords: error messages, file paths, component names
2. Read the appropriate documentation based on the issue type above
3. Navigate to source code only if docs don't fully answer the question
