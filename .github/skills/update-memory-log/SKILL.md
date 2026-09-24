---
name: update-memory-log
description: Append a correctly formatted entry to MEMORY.md. Use after completing a task that produced a durable lesson, or when correcting an earlier memory entry.
---

# Update memory log

`MEMORY.md` is append-only (PROTOCOL.md, Article IV). This skill appends a
schema-compliant entry.

## Steps

1. Confirm the lesson is **durable**: a fact, convention, or mistake worth
   remembering across sessions. Skip temporary or task-specific details.
2. Open `MEMORY.md` and append to the **end of the Log section** (newest
   last) using exactly this format:

   ```markdown
   ### YYYY-MM-DD — <short title>
   - **Task:** what was being done
   - **Lesson:** the durable fact or lesson learned
   - **Citation:** file:line, PR/commit reference, or `User input: "<quote>"`
   ```

3. Never edit or delete existing entries. To correct one, append a new entry
   whose Lesson starts with `Supersedes <date> — <title>:`.
4. Never include secrets, credentials, or personal data.
5. Commit the change with a message like `Log memory: <short title>`.
