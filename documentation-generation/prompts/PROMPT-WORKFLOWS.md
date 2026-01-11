# Prompt: Generate Workflow Documentation

> **Output:** `WORKFLOWS.md`

---

## The Prompt

````text
You are documenting the key business workflows in a software project. First, 
detect the language/framework used, then analyze the codebase and write 
WORKFLOWS.md that explains how the major processes work end-to-end.

## Before You Start

Create a notes file at `{ProjectName}.WORKFLOWS.notes.md` and build it
incrementally as you read each file. This protects against context limits.

**For each service/controller/handler file in the project:**

1. Read the file in its ENTIRETY - do not read partial line ranges
2. Immediately append notes for workflows found to `{ProjectName}.WORKFLOWS.notes.md`
3. Move to the next file

**Notes format for each workflow discovered:**

```
### WorkflowName (e.g., "User Registration")
- **Trigger**: What starts it (endpoint, event, job)
- **Entry point**: File/class and method/function
- **Steps**: Numbered list of what happens
- **Services involved**: List of modules/classes called
- **Data read/written**: What entities are accessed
- **External calls**: APIs, queues, other systems
- **Error handling**: How failures are handled
- **Output**: What gets returned/published/saved
```

If you cannot read a file completely, note that in the file entry.

After all files are processed, use the notes to write the final documentation.

## Writing the Documentation

Write for a developer who needs to:
- Debug issues in a process
- Modify or extend existing workflows
- Understand what happens when a user performs an action

Focus on the important workflows that drive the business, not every code path.

Project: {ProjectName}

---

Structure your document roughly like this (adapt as needed):

# Workflows

## Overview
What are the main things this system does? Brief context.

## [Workflow Name]

### What Triggers It
User action, API call, scheduled job, event from another system, etc.

### What Happens
Step-by-step walkthrough of the process. What services are involved, what 
order things happen, where data is read/written.

### What Can Go Wrong
Common failure points. What happens when external services are down? What 
errors can occur and how are they handled?

### What Gets Produced
Events published, notifications sent, data created/modified, responses returned.

(Repeat for each major workflow)

## Background Processes
Any scheduled jobs, queue processors, or async workflows. When do they run? 
What do they do?

## Integration Points
Where this system touches other systems. Events it publishes or subscribes to.
APIs it calls or exposes.

---

## Files Analyzed

At the end of the document, include:

- **Fully read**: [list files you completely analyzed]
- **Partially read**: [list files that were too large to fully read]
- **Skipped**: [list any files not accessed, and why]
````

---

## Tips

- Look at route handlers, controllers, command handlers, and service methods
- Follow the code path through to understand the full flow
- Error handling paths are often as important as happy paths
