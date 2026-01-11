# Prompt: Generate Data Documentation

> **Output:** `DATA.md`

---

## The Prompt

````text
You are documenting the data model for a software project. First, detect the 
language/framework and ORM/data access patterns used, then analyze the codebase 
and write the DATA.md that explains the entities, relationships, and database 
schema.

## Before You Start

Create a notes file at `{ProjectName}.DATA.notes.md` and build it
incrementally as you read each file. This protects against context limits.

**For each entity/model file in the project:**

1. Read the file in its ENTIRETY - do not read partial line ranges
2. Immediately append notes for that file to `{ProjectName}.DATA.notes.md`
3. Move to the next file

**Notes format for each entity:**

```
### EntityName.ext
- **Table**: Table name if known
- **Properties/Fields**: List with types and constraints
- **Relationships**: Foreign keys, references, associations
- **Validation**: Validation rules, constraints
- **Notes**: Anything notable (computed fields, inheritance, etc.)
```

Also note ORM configurations, repository patterns, and data access classes.

If you cannot read a file completely, note that in the file entry.

After all files are processed, use the notes to write the final documentation.

## Writing the Documentation

Write for a developer who needs to:
- Understand what data the system manages
- Write queries or modify entities
- Understand why the data is structured this way

Project: {ProjectName}

---

Structure your document roughly like this (adapt as needed):

# Data Model

## Overview
What kind of data does this system manage? Brief context.

## Entities

### [EntityName]
What it represents in business terms. Key fields and what they mean.
Important relationships to other entities.
Any validation rules or constraints.
Common queries or access patterns.

(Repeat for each significant entity)

## Relationships
How entities connect. Include a simple diagram if relationships are complex:

```
Order ──< OrderItem >── Product
  │
  └── Customer
```

## Database Details
- What database engine(s)
- ORM/data access approach
- Any important indexes
- Soft deletes, audit fields, or other patterns used
- Migration strategy if relevant

## Data Flows
How does data enter the system? How is it modified? Any batch processes?

## Gotchas
Anything surprising or non-obvious about the data model. Things that have 
caused bugs or confusion in the past.

---

## Files Analyzed

At the end of the document, include:

- **Fully read**: [list files you completely analyzed]
- **Partially read**: [list files that were too large to fully read]
- **Skipped**: [list any files not accessed, and why]
````

---

## Tips

- Look for model/entity folders, ORM configurations, and migration files
- Schema definition files and database configs are useful sources
- Include business context - "Order" means more than just the fields
