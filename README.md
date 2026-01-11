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
│   └── database/
│       ├── schema/                # Tables, indexes, constraints, views
│       ├── procedures/            # Stored procedures, functions, triggers
│       └── seed-data/             # INSERT scripts, reference data
│
├── documentation-generation/
│   ├── prompts/                   # Prompt templates
│   │   └── Initial-prompt.md      # Entry point for AI agent
│   ├── output/                    # Generated documentation
│   └── README.md                  # Detailed prompt usage guide
│
└── .github/
    └── copilot-instructions.md    # Instructions for GitHub Copilot
```

## What Gets Generated

For each project:

| Document            | Contains                             |
| ------------------- | ------------------------------------ |
| `ARCHITECTURE.md`   | System design, components, decisions |
| `DATA.md`           | Entities, relationships, schema      |
| `WORKFLOWS.md`      | Business processes, data flows       |
| `API.md`            | REST endpoints, authentication       |
| `CONFIGURATION.md`  | Settings, secrets, setup             |

For multi-project repositories:

| Document       | Contains                                    |
| -------------- | ------------------------------------------- |
| `SOLUTION.md`  | Overview, project relationships, key flows  |

## Using with GitHub Copilot

The `.github/copilot-instructions.md` file provides context automatically.

**Recommended Model:** Claude Sonnet 4.5 or better for optimal results.

**To generate documentation:**

1. Open `documentation-generation/prompts/Initial-prompt.md`
2. Ask Copilot to follow the instructions in the file
3. Documentation will be generated in `documentation-generation/output/`

## Using Generated Documentation for Troubleshooting

Once documentation is generated, you can use it to help AI understand your
codebase when debugging issues.

**When you encounter a bug or need to understand behavior:**

1. Provide the relevant documentation files to the AI:
   - `ARCHITECTURE.md` - For understanding system design and component roles
   - `DATA.md` - For entity relationships and database issues
   - `WORKFLOWS.md` - For tracing business process flow
   - `CONFIGURATION.md` - For environment and settings issues

2. Describe the problem:
   - Error message or unexpected behavior
   - What you expected to happen
   - Steps to reproduce

**Why this works:**

The documentation tells the AI *where* to look - which modules, services, and
workflows are involved. The error message tells it *what* to look for. The AI
can then navigate to the relevant code files itself based on this context.

You don't need to paste code snippets - the AI has access to your codebase and
can locate the files mentioned in the documentation and error message.

**Tips for effective troubleshooting:**

- Start with `ARCHITECTURE.md` for any issue - it provides essential context
- Add `DATA.md` when the issue involves entities or database operations
- Add `WORKFLOWS.md` when tracing a multi-step process
- Only include what's relevant - don't overload with all documentation

## Customization

- Edit prompts in `documentation-generation/prompts/` to match your needs
- Add custom sections for compliance, security, or domain-specific docs
- Modify `.github/copilot-instructions.md` for tool-specific behavior
