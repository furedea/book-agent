---
description: Generate a new subagent definition from the notes of a single technical resource
allowed-tools: Bash, Read, Write, Glob
model: claude-sonnet-4-20250514
---

# Subagent Generation

Generate a complete sub-agent definition file based on the notes from a technical resource.

## Tasks

### Phase 1: Analyze Technical Resource

- Technical resource: $ARGUMENTS
- Analyze the notes excluding metadata such as title or author to identify the main subject and key concepts.

### Phase 2: Generate Agent Name

- Generate a concise, descriptive `agent-name` based on the overall subject identified from the analysis.

Note: Avoid deriving the `agent-name` directly from the source's title because the title is not always a reliable indicator of the main subject.

### Phase3: Generate Subagent Definition Draft

- Generate the complete subagent definition draft in English, following `#### Subagent Definition Structure` below.

#### Subagent Definition Structure

```markdown
---
name: {agent-name}
description: Expert for code and design reviews and improvement suggestions based on a specific knowledge base
tools: Bash, Read, Write, Edit, MultiEdit, Glob, Grep
---

# Role

You are an expert on {agent-name}. Provide analysis, review, and improvement suggestions strictly based on the principles and techniques described in the knowledge base below.

## Knowledge Base

### 1. Summary

{A summary of the analyzed context in about three sentences}

### 2. Core Principles

- {Principle 1}: {Brief explanation}
- {Principle 2}: {Brief explanation}
- ...

### 3. Key Techniques and Patterns

- {Technique 1}: {Brief explanation}
- {Technique 2}: {Brief explanation}
- ...

### 4. Anti-patterns and Pitfalls to Avoid

- {Anti-pattern 1}: {Brief explanation and why it is problematic}
- {Anti-pattern 2}: {Brief explanation and why it is problematic}
- ...

## Directives

1. Scope: Base all reasoning and suggestions strictly on the provided knowledge. Do not use external knowledge.
2. Interaction: When asked for a review, first state the main principles from this knowledge base.
3. Output: Provide actionable feedback. Suggest specific code or design changes, and explain why your suggestions align with the philosophy of the knowledge base.
```

#### Note

- If the structure of the provided technical resource does not align well with the Knowledge Base template above (e.g., it is not organized into Core Principles, Techniques, etc.), you are permitted to adapt or replace the headings within the `## Knowledge Base` section only. In such cases, create a new logical structure that is more faithful to the source document's organization, such as being based on its main chapters or core ideas.
- Refrain from using bold formatting (`**`). Instead, use clear and well-structured sentences to convey importance.

### Phase 4: Check for Auto-Approval Flag

- If $ARGUMENTS contains a `-y` flag, skip the interactive approval and proceed directly to PHASE 7.

### Phase 5: Present Draft and Request Approval

Present the draft to the user for review. Output the following four items clearly:

1. The generated `agent-name` and reasoning
2. A concise context summary
3. The full content of the generated subagent definition draft
4. you MUST ask the user for confirmation with the question:

```
----------------------------------------
Please review the generated draft. Do you approve?
[1] Approve (enter 'y')
[2] Edit (enter your modifications directly)
----------------------------------------
Your input:
```

Phase 6: Wait for User Input and Act Accordingly

Stop and wait for the user's response. Based on their input, follow one of these paths:

- If the user approves (e.g., "y" or "yes"): Proceed to PHASE 6.
- If the user requests modifications (e.g., "change the name to X", "add principle Y"): Acknowledge the request, return to Phase 1 to regenerate the draft with the requested changes, and then proceed through all phases

Phase 7: Save the File

Upon approval, save the subagent definition content to the file.

1. If `./.claude/agents/book-agent/` directory does not exist, create it
2. Check for name conflicts for the `./.claude/agents/book-agent/{agent-name}.md` file. If a conflict exists, append a numeric suffix (e.g., `./.claude/agents/book-agent/{agent-name}_2.md`)
3. Write the content to the resolved file path
4. the process by printing a success message
