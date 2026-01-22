# Documentation Generation Workspace

A template workspace for generating AI-friendly documentation from software projects.
Works with any language or framework.

## Quick Start

1. **Add your application:**
   - Copy your project/repository to `application/source/`
   - Optionally add database files to the appropriate folders

2. **Generate documentation:**
   - Open `documentation-generation/prompts/Initial-prompt.md`
   - Point your AI agent to this file
   - Documentation will be generated in `documentation-generation/output/`

## Folder Structure

```text
├── application/
│   ├── source/                    # Your project/repository goes here
│   └── databases/                 # Add subfolders for each database technology
│       └── {database-type}/       # e.g., mysql/, postgres/, db2/, mongodb/
│           ├── schema/            # Tables, indexes, constraints, views
│           ├── procedures/        # Stored procedures, functions, triggers
│           └── seed-data/         # INSERT scripts, reference data
│
├── documentation-generation/
│   ├── prompts/                   # Prompt templates
│   │   └── Initial-prompt.md      # Entry point for AI agent
│   ├── output/                    # Generated documentation
│   │   ├── {ProjectName}/         # Docs for each project
│   │   └── _notes/                # Working notes (deletable after)
│   │       └── {ProjectName}/     # Notes organized by project
│   └── README.md                  # Detailed prompt usage guide
│
└── .github/
    └── copilot-instructions.md    # Instructions for GitHub Copilot
```

### Setting Up Database Folders

Create subfolders under `databases/` for each database technology your project uses:

```text
# Single database example
databases/
└── postgres/
    ├── schema/
    ├── procedures/
    └── seed-data/

# Multiple databases example
databases/
├── mysql/
│   ├── schema/
│   └── seed-data/
└── db2/
    └── procedures/
```

After creating your folders, update the "Additional Resources" table in
`documentation-generation/prompts/Initial-prompt.md` to match your structure.

## What Gets Generated

For each project:

| Document           | Contains                               |
| ------------------ | -------------------------------------- |
| `ARCHITECTURE.md`  | System design, components, decisions   |
| `DATA.md`          | Entities, relationships, schema        |
| `WORKFLOWS.md`     | Business processes, data flows         |
| `API.md`           | REST endpoints, authentication         |
| `CONFIGURATION.md` | Settings, secrets, setup               |
| `SECURITY.md`      | Auth flows, data protection (optional) |
| `DEPENDENCIES.md`  | Packages, licenses, rationale (optional)|

For multi-project repositories:

| Document        | Contains                                   |
| --------------- | ------------------------------------------ |
| `REPOSITORY.md` | Overview, project relationships, key flows |

### Working Notes

During generation, the AI creates incremental notes in `output/_notes/{ProjectName}/`.
These protect against context limits and help troubleshoot incomplete output. They can
be safely deleted after documentation is finalized.

## Using with GitHub Copilot

The `.github/copilot-instructions.md` file provides context automatically.

**Recommended Model:** Claude Sonnet 4.5 or better for optimal results.

**To generate documentation:**

1. Open `documentation-generation/prompts/Initial-prompt.md`
2. Ask Copilot to follow the instructions in the file
3. Documentation will be generated in `documentation-generation/output/`

## Using Generated Documentation for Troubleshooting

Once documentation is generated, the AI can use it to understand your codebase
when helping with questions or debugging issues.

### How Navigation Works

The AI follows a path from general to specific, loading only what's needed:

1. **REPOSITORY.md** (multi-project repos) → Identifies which project(s) are involved
2. **ARCHITECTURE.md** → Provides the component map for that project
3. **Specific doc** → Based on the issue type (see below)
4. **Source code** → Only if docs don't fully answer the question

This keeps context focused and avoids confusion from loading everything at once.

### Which Document for Which Problem

| Issue Type                          | Start With                        |
| ----------------------------------- | --------------------------------- |
| Understanding a component           | ARCHITECTURE.md                   |
| Entity/database errors              | ARCHITECTURE.md → DATA.md         |
| Process not completing correctly    | ARCHITECTURE.md → WORKFLOWS.md    |
| API call failing, wrong response    | ARCHITECTURE.md → API.md          |
| Startup failures, missing config    | CONFIGURATION.md                  |
| Auth/permission denied errors       | ARCHITECTURE.md → SECURITY.md     |
| Package conflicts, version issues   | DEPENDENCIES.md                   |
| Cross-project issues                | REPOSITORY.md → relevant projects |

### How to Ask for Help

1. **Describe the problem:**
   - Error message or unexpected behavior
   - What you expected to happen
   - Steps to reproduce (if applicable)

2. **Let the AI navigate:** The AI will read the appropriate documentation
   files based on your description, then dive into source code if needed.

You don't need to manually attach documentation files or paste code snippets.
The AI has access to your codebase and will locate the relevant files based
on the documentation and your error message.

## Copying to Your Repository

Once generated, you can copy the documentation into your actual project:

```text
your-repository/
├── REPOSITORY.md            ← Repository overview (for multi-project)
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

## Maintenance

Regenerate documentation when:

- Major architectural changes occur
- New entities or workflows are added
- API contracts change significantly

Small changes can often be manually edited - these are meant to be living
documents, not generated artifacts.

## Limitations

This documentation captures what can be learned from reading the code. It won't include:

- **Runtime behavior** - Performance characteristics, actual load patterns, or timing issues
- **Tribal knowledge** - Undocumented decisions, workarounds, or "why we don't touch that code"
- **Historical context** - Why certain bugs exist, failed approaches that were tried before
- **External dependencies** - How third-party services actually behave vs. their documentation

For these, you'll still need team knowledge or additional context when troubleshooting.

## Customization

- Edit prompts in `documentation-generation/prompts/` to match your needs
- Add custom sections for compliance, security, or domain-specific docs
- Modify `.github/copilot-instructions.md` for tool-specific behavior
