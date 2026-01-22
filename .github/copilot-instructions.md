# Copilot Instructions

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
    ├── output/                    # Generated docs (ARCHITECTURE, DATA, API, etc.)
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
- For files over 500 lines, read in chunks and append findings to notes files as you go
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

| If project contains...              | It's likely a...       | Run these prompts                 |
| ----------------------------------- | ---------------------- | --------------------------------- |
| Route handlers, API endpoints       | Web API                | All (including SECURITY, DEPS)    |
| ORM models, repositories            | Data access layer      | ARCH, DATA, CONFIG                |
| Services, commands, business logic  | Business logic library | ARCH, DATA, WORKFLOWS, CONFIG     |
| Workers, schedulers, queue handlers | Background service     | ARCH, DATA, WORKFLOWS, CONFIG     |
| Utilities, helpers, extensions      | Utility library        | ARCH, CONFIG, DEPENDENCIES        |
| CLI commands, argument parsing      | CLI tool               | ARCH, CONFIG                      |
| Components, pages, routes (UI)      | Frontend app           | ARCH, WORKFLOWS, CONFIG, SECURITY |

## When Asked to Help with Code Questions or Troubleshooting

If documentation exists in `documentation-generation/output/`:

1. **Start with the index**: Read `REPOSITORY.md` first (if it exists) to understand what projects exist and how they relate. For single-project repos, skip to step 3.
2. **Identify the relevant project(s)**: Based on the question, error message, or file paths mentioned, determine which project(s) are involved.
3. **Read ARCHITECTURE.md for that project**: This gives you the component map and helps narrow down where to look.
4. **Then read the specific doc based on the issue type**:
   - Entity/database errors → DATA.md
   - Process not completing, wrong behavior → WORKFLOWS.md
   - API call failing, wrong response → API.md
   - Startup failures, missing config → CONFIGURATION.md
   - Auth/permission denied errors → SECURITY.md
   - Package conflicts, version issues → DEPENDENCIES.md
5. **Only then dive into source code** if the docs don't fully answer the question.

This navigation pattern (index → architecture → specific topic) loads 2-3 focused documents instead of everything, keeping context clear and accurate.
