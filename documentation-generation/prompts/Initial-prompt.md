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

When you need deeper context beyond the source code:

| Resource       | Location                          | Use For                        |
| -------------- | --------------------------------- | ------------------------------ |
| DB Schema      | `../application/database/schema/`     | Table definitions, views   |
| DB Procedures  | `../application/database/procedures/` | Stored procs, functions    |
| DB Seed Data   | `../application/database/seed-data/`  | Default values, lookups    |

Reference these when documenting:

- DATA.md → Check schema and seed data folders
- WORKFLOWS.md → Check procedures for business logic
- CONFIGURATION.md → Check for connection strings and settings

## Execution Order

1. List all projects in `../application/source/`
2. Detect the language/framework for each project
3. Determine project type (API, library, worker, etc.)
4. Run the appropriate prompts per the README guidance
5. Save outputs to `../output/{ProjectName}/`
6. Run `PROMPT-SOLUTION.md` **last** (after all projects are documented)

## Verification

After completing each project, confirm:

- [ ] All relevant prompts were run for the project type
- [ ] Files are saved in correct output folder
- [ ] "Files Analyzed" section is included in each document
- [ ] Markdown follows rules in `.markdownlint.json` (blank lines around headings/lists/code blocks, spaces in tables)
