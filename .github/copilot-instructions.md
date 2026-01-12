# Copilot Instructions

**Recommended Model:** Claude Sonnet 4.5 or better for optimal results.

This workspace is for generating documentation for software projects.
It works with any language or framework.

## Workspace Structure

```text
├── application/
│   ├── source/                    # Project source code
│   └── databases/                 # Database resources (customizable)
│       └── {db-type}/             # e.g., mysql/, postgres/, db2/
│           ├── schema/            # Tables, indexes, constraints, views
│           ├── procedures/        # Stored procedures, functions, triggers
│           └── seed-data/         # INSERT scripts, reference data
│
└── documentation-generation/
    ├── prompts/                   # Documentation generation prompts
    │   └── Initial-prompt.md      # START HERE
    ├── output/                    # Generated documentation
    └── README.md                  # Prompt usage guide
```

**Note:** The `databases/` folder structure is customizable. Check `Initial-prompt.md`
for the actual folder locations configured for this project.

## When Asked to Generate Documentation

1. Start by reading `documentation-generation/prompts/Initial-prompt.md`
2. Follow the instructions there - it points to the README and other resources
3. Save all output to `documentation-generation/output/{ProjectName}/`

## Key Rules

- Always read the full content of code files before documenting
- For files over 200 lines, confirm complete reading
- Include "Files Analyzed" section at end of each document
- Reference database folders when documenting DATA.md and WORKFLOWS.md
- Run PROMPT-REPOSITORY.md last, after all projects are documented

## Markdown Formatting Rules

Follow these rules strictly when generating markdown:

1. **Blank lines**: Add a blank line before and after headings, lists, and code blocks
2. **Lists**: Use `-` for unordered lists, maintain consistent indentation (2 spaces)
3. **Tables**: Add spaces around pipe characters: `| Cell |` not `|Cell|`
4. **Code blocks**: Always specify a language (e.g., `python`, `javascript`, `json`)
5. **Line length**: Keep lines under 100 characters where practical
6. **Headings**: Use ATX style (`#`, `##`) not underlines, don't skip levels
7. **Trailing spaces**: No trailing whitespace at end of lines
8. **Final newline**: End files with a single newline character

Reference `.markdownlint.json` in the workspace root for the full configuration.

## Project Type Detection

First, detect the language/framework from the codebase, then determine type:

| If project contains...              | It's likely a...       | Run these prompts          |
| ----------------------------------- | ---------------------- | -------------------------- |
| Route handlers, API endpoints       | Web API                | All prompts                |
| ORM models, repositories            | Data access layer      | ARCH, DATA, CONFIG         |
| Services, commands, business logic  | Business logic library | ARCH, DATA, WORKFLOWS, CFG |
| Workers, schedulers, queue handlers | Background service     | ARCH, DATA, WORKFLOWS, CFG |
| Utilities, helpers, extensions      | Utility library        | ARCH, CONFIG only          |
| CLI commands, argument parsing      | CLI tool               | ARCH, CONFIG               |
| Components, pages, routes (UI)      | Frontend app           | ARCH, WORKFLOWS, CONFIG    |
