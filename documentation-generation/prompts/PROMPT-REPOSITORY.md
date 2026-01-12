# Prompt: Generate Repository Overview

> **Output:** `REPOSITORY.md`
> **Use for:** Multi-project/multi-package repositories

---

## The Prompt

````text
You are documenting a multi-project repository. First, detect the languages 
and frameworks used, then analyze the structure and write REPOSITORY.md that 
explains how all the pieces fit together.

## Before You Start

Create a notes file at `../output/_notes/{RepositoryName}/REPOSITORY.notes.md` and
build it incrementally as you review each project. This protects against context limits.

**For each project/package in the repository:**

1. Read the project manifest (package.json, pom.xml, .csproj, Cargo.toml, etc.)
2. Read the project's ARCHITECTURE.md if it exists
3. Immediately append notes for that project to `../output/_notes/{RepositoryName}/REPOSITORY.notes.md`
4. Move to the next project

**Notes format:**

```
### Projects Inventory
- ProjectName: Type (API/Library/Worker/CLI), primary purpose

### Dependency Graph
- ProjectA depends on: ProjectB, ProjectC
- ProjectB depends on: ProjectD

### Key Flows (from ARCHITECTURE.md files)
- Flow name: Projects involved, brief description

### Shared Code
- SharedProject: What it contains, who uses it

### Entry Points
- Which project(s) to run
- Startup dependencies
```

If you cannot read a file completely, note that in the file entry.

After all projects are processed, use the notes to write the final documentation.

## Writing the Documentation

Write for a developer who is new to this codebase and needs to understand:
- What this system does overall
- Which project to look at for what
- How the projects depend on each other
- Where to start when making changes

Project: {RepositoryName}

---

Structure your document roughly like this (adapt as needed):

# Repository Overview

## What Is This?
2-3 sentences on what this system does from a business perspective.

## Tech Stack
Languages, frameworks, and key shared technologies across projects.

## Projects

### [ProjectName]
One paragraph: what it does, what type of project (API, library, worker, CLI), 
and when you'd need to work in it.

(Repeat for each project)

## How They Fit Together
Explain the relationships. A simple diagram helps:

```
┌─────────────┐     ┌─────────────────┐
│   Web API   │────▶│   Core Logic    │
└─────────────┘     └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │   Data Access   │
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │     Shared      │
                    └─────────────────┘
```

## Key Flows
Brief description of 2-3 main things the system does and which projects 
are involved in each.

## Shared Code
What's in shared/common projects and when to use them.

## Getting Started
Which project to run, how to run it, what dependencies are needed.

## Documentation Index
Links to each project's documentation:
- [Web.API](./Web.API/ARCHITECTURE.md)
- [Core](./Core/ARCHITECTURE.md)
- etc.

---

## Files Analyzed

At the end of the document, include:

- **Fully read**: [list projects/files you completely analyzed]
- **Partially read**: [list files where the notes file was used instead of complete reading]
- **Skipped**: [list any projects/files not accessed, and why]
````

---

## Tips

- Run this after documenting individual projects
- Focus on the relationships, not duplicating project-level details
- The diagram doesn't need to be fancy - ASCII works fine
