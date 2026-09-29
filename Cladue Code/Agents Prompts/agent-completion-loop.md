# Agent completion loop

A short prompt I add to the end of a project prompt to help agents keep working through implementation, verification, and delivery. It can be edited to fit the project and tools being used.

This is an instruction, not an automatic restart mechanism. If a session ends, resume it using the project's checkpoint.

## Copy and paste

<!-- Add the paragraph below to the END of your main project prompt. -->
<!-- Edit it to match your workflow. Keep the verification and authorization boundaries. -->

```text
Continue the authorized task until all agreed deliverables are implemented, integrated, verified, and delivered—not merely planned or partially built. Repeat: inspect current state → select unfinished work → execute or delegate → verify → fix failures → update the task ledger and project memory. The coordinator owns overall completion; an agent handoff is not project completion. Make routine, reversible decisions without repeatedly asking to continue. If blocked, investigate, try a justified alternative, and finish unaffected work; avoid repeating failed approaches indefinitely. Before interruption or context exhaustion, save completed work, verification evidence, blockers, and the exact next action; resume from that checkpoint. Never invent successful checks, silently reduce scope, or exceed authorization. Finish only when requirements are satisfied, or report the concrete external blocker and what is needed to proceed.
```

## How I use it

1. Write the main project prompt first: goal, deliverables, scope, constraints, and what counts as complete.
2. Copy the paragraph above and append it after those instructions.
3. Edit the references below to match the actual project. This prompt does not replace clear requirements.
4. Run the task. If the session stops, use the resume instruction at the bottom.

## What to change

| Your setup | Change | Example replacement |
|---|---|---|
| One agent | Replace the coordinator sentence | `You own completion from implementation through verification and delivery.` |
| No delegation tools | Replace `execute or delegate` | `execute` |
| Named task and memory files | Replace `the task ledger and project memory` | `TASKS.md and BRAIN.md` |
| Existing issue tracker | Replace `the task ledger` | `the project's issue tracker` |
| Document or research task | Replace `implemented, integrated, verified, and delivered` | `completed, checked against the requirements, and delivered` |
| Specific completion checks | Add a sentence at the end | `Completion requires the Android build, API integration tests, and local startup checks to pass.` |
| Restricted environment | Add a sentence at the end | `Keep all runtime services local and use fictional data only.` |

Only name files, tools, and checks that actually apply. For small tasks, a short progress note is enough; separate tracking files are optional.

## Example customization

For a coding project with one agent and local tracking files, change:

```text
execute or delegate → execute
the task ledger and project memory → TASKS.md and BRAIN.md
The coordinator owns overall completion; an agent handoff is not project completion.
→ You own completion from implementation through verification and delivery.
```

Then append the project's actual completion checks. Keep the instructions to report honest evidence, preserve scope, and respect authorization.

## Resume instruction

```text
Restore the project checkpoint and task ledger. Verify the current workspace, then continue the completion loop from the next unfinished requirement.
```

If you renamed the tracking files, name those files in the resume instruction too.
