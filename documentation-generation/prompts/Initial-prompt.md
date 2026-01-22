# Documentation Generation Instructions

## Objective

Generate standard documentation for all projects in `../application/source/`.

## How to Start

1. Read the [README.md](../README.md) first - it explains which prompts to run
   for each project type
2. Return here for file locations and execution steps

## Source Location

```text
../application/source/{ProjectName}/
```

**Note:** Replace `{ProjectName}` with the folder name of the project you're documenting
(e.g., `api-service`, `core-library`). Use this same name consistently in output paths and
notes files.

## Output Location

Save all generated files to:

```text
../output/{ProjectName}/{OutputFile}.md
```

**Example:**

```text
../output/api-service/ARCHITECTURE.md
../output/api-service/DATA.md
../output/api-service/WORKFLOWS.md
../output/api-service/API.md
../output/api-service/CONFIGURATION.md
```

## Additional Resources

When you need deeper context beyond the source code, check the `databases/` folder.

**Default structure** (customize for your project):

| Resource       | Location                                    | Use For                  |
| -------------- | ------------------------------------------- | ------------------------ |
| DB Schema      | `../application/databases/{db-type}/schema/`    | Table definitions, views |
| DB Procedures  | `../application/databases/{db-type}/procedures/`| Stored procs, functions  |
| DB Seed Data   | `../application/databases/{db-type}/seed-data/` | Default values, lookups  |

**⚠️ Important:** Update this table to match your actual folder structure. Examples:

Single database (PostgreSQL):

| Resource       | Location                                   | Use For                  |
| -------------- | ------------------------------------------ | ------------------------ |
| Schema         | `../application/databases/postgres/schema/`    | Table definitions    |
| Seed Data      | `../application/databases/postgres/seed-data/` | Reference data       |

Multiple databases (MySQL + DB2):

| Resource       | Location                                   | Use For                  |
| -------------- | ------------------------------------------ | ------------------------ |
| MySQL Schema   | `../application/databases/mysql/schema/`       | Table definitions    |
| MySQL Seed     | `../application/databases/mysql/seed-data/`    | Reference data       |
| DB2 Procedures | `../application/databases/db2/procedures/`     | Mainframe operations |

Reference these when documenting:

- DATA.md → Check schema and seed data folders
- WORKFLOWS.md → Check procedures for business logic
- CONFIGURATION.md → Check for connection strings and settings

## Files to Skip

Do not attempt to read or document these file types:

- **Dependency folders**: `node_modules/`, `vendor/`, `packages/`, `.nuget/`
- **Build output**: `dist/`, `build/`, `bin/`, `obj/`, `out/`, `target/`
- **Minified files**: `*.min.js`, `*.min.css`, `*.bundle.js`
- **Binary files**: images, fonts, compiled files, archives
- **Lock files**: `package-lock.json`, `yarn.lock`, `Cargo.lock`, `poetry.lock`
- **Generated code**: files marked as auto-generated, `.designer.cs`, `*.g.cs`
- **IDE/editor files**: `.idea/`, `.vscode/` (except settings you need), `*.suo`

If you encounter a file you cannot parse, note it in the "Skipped" section with the reason.

## Execution Order

1. List all projects in `../application/source/`
2. Detect the language/framework for each project
3. Determine project type (API, library, worker, etc.)
4. Run the appropriate prompts per the README guidance
5. Save outputs to `../output/{ProjectName}/`
6. Run `PROMPT-REPOSITORY.md` **last** (after all projects are documented)

## Verification

After completing each document, run this self-check before moving to the next prompt:

### Document Quality Check

- [ ] **Completeness**: Does the document cover all major aspects for its type?
  - ARCHITECTURE: Overview, tech stack, key components, how it works, design decisions
  - DATA: Entities, relationships, database details, data flows
  - WORKFLOWS: Major processes with triggers, steps, error handling, outputs
  - API: Authentication, endpoints with parameters/responses/errors
  - CONFIGURATION: Required settings, environment variables, local setup steps
  - SECURITY: Auth methods, authorization model, data protection, input validation
  - DEPENDENCIES: Runtime/dev packages with versions, licenses, rationale
- [ ] **Files Analyzed section**: Is it present at the end with fully read/partially read/skipped?
- [ ] **Specificity**: Does it reference actual file names, class names, and code patterns from this project (not generic placeholders)?
- [ ] **Readability**: Would a new developer understand this without reading the code first?

### Technical Check

- [ ] **Markdown formatting**: Blank lines around headings/lists/code blocks, spaces in tables
- [ ] **Output location**: File saved to `../output/{ProjectName}/`
- [ ] **Notes file**: Incremental notes saved to `../output/_notes/{ProjectName}/`

### After All Projects Complete

- [ ] All relevant prompts were run for each project type
- [ ] PROMPT-REPOSITORY.md was run last (for multi-project repos)
- [ ] Cross-references between documents are consistent
