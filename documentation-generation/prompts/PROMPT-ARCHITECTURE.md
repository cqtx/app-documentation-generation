# Prompt: Generate Architecture Documentation

> **Output:** `ARCHITECTURE.md`

---

## The Prompt

````text
You are a senior developer documenting a software project for your team. First,
detect the language/framework used in this codebase, then analyze it and write
the ARCHITECTURE.md that should have been created when the project was built.

## Before You Start

Create a notes file at `../output/_notes/{ProjectName}/ARCHITECTURE.notes.md` and
build it incrementally as you read each file. This protects against context limits.

**For each source code file in the project:**

1. Read the file in its ENTIRETY - do not read partial line ranges
2. Immediately append notes for that file to `../output/_notes/{ProjectName}/ARCHITECTURE.notes.md`
3. Move to the next file

**Notes format for each file:**

```
### FileName.ext
- **Purpose**: One sentence
- **Key classes/functions**: List them
- **Dependencies**: What it imports/injects/uses
- **Public interface**: List with one-line descriptions
- **Calls**: What other modules/services it calls
- **Notes**: Anything notable (patterns, complexity, concerns)
```

**Also check** the `../application/databases/` folder structure (see Initial-prompt.md) for:
- Schema files → Database architecture
- Procedures → Database-tier components

If you cannot read a file completely, note that in the file entry.

After all files are processed, use the notes to write the final documentation.

## Writing the Documentation

Write for a new developer joining the team. They understand the language but 
know nothing about this project. Focus on helping them understand:

- What this project does and why it exists
- How the major pieces fit together
- Why key technical decisions were made
- Where to look when they need to change something

Be conversational and practical. This is internal documentation, not a formal 
specification.

Project: {ProjectName}

---

Structure your document roughly like this (adapt as needed):

# Architecture

## Overview
What does this project do? Why does it exist? Where does it fit in the larger 
system?

## Tech Stack
Language, framework, key libraries, and why they were chosen.

## Key Components
The major classes/modules/services and what they're responsible for. Focus on 
the important ones, not every file.

## How It Works
Walk through the main flow(s). How does data come in, get processed, and go out?

## Design Decisions
Any non-obvious choices and why they were made. Things a new developer might 
question or need to understand.

## Dependencies
What external services, databases, or libraries does this rely on? Why those 
choices?

Check the `databases/` folder structure (see Initial-prompt.md) for database-related
dependencies and constraints.

## Boundaries
What this project is NOT responsible for. Where does it hand off to other 
systems?

## Common Tasks
Brief pointers for: "If you need to add X, look here" or "To change Y, 
you'll need to understand Z first."

---

## Files Analyzed

At the end of the document, include:

- **Fully read**: [list files you completely analyzed]
- **Partially read**: [list files where the notes file was used instead of complete reading]
- **Skipped**: [list any files not accessed, and why]
````

---

## Tips

- Let the AI discover the architecture from the code
- If it misses something important, ask follow-up questions
- The output should read like a human wrote it, not a template filled in
