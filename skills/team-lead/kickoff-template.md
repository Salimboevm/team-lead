# Kickoff prompt template

Paste this into a fresh Claude Code session running Opus, after filling in every `<placeholder>`. Delete any line that doesn't apply.

---

Build <feature> from the frozen design pack. Load the team-lead skill first and follow it. You are the Opus lead, a senior manager, at high effort. `fable-reviewer` is the C-suite that audits your work. `sonnet-engineer` is the team that builds. I decide everything.

Go deeper, not bigger. The pack is frozen and is the source of truth: no new features, no new design. Any difference you find between the pack and reality is reported to me, never fixed silently.

The pack (in `<path to pack>`; read it there and never copy it into a repo):
- the spec: `<spec file>`;
- the delivery plan: `<plan file>`, with <n> epics and <n> ACs, each with its scenario ids;
- the diagrams: `<diagram files>`;
- the risk list: `<risk file and heading>`;
- the decision record: `<decision file and section>`;
- the test oracle: `<oracle file or replay script>`. Run it with `<check command>` only.

Branches: `<repo>` is on `<branch>`, created by me. Check with `git branch --show-current` before every brief. Never switch or create branches, and stop if a branch differs.

The code goes in:
- `<repo 1>`: `<what goes there>`;
- `<repo 2>`: `<what goes there>`.

Batches:
- **Core:** `<epics in the first batch>`.
- **Then:** `<remaining epics, in order>`, unless the inventory shows a better order.

Project rules: `<list them here, or point to CLAUDE.md>`.

1. **Inventory.** Before any code, map what already exists for this feature in every repo, with each file's authors. Build a collision map against the core batch: what we reuse, what we add beside it, and what a later epic replaces. List every file owned by someone else that would change, with what would change in it, and give me that list to approve. The team may edit only the files I approve. Report the whole inventory to me.
2. **Blockers.** Some risks block a core slice. Bring each one to me before its slice is briefed, two at a time, with Fable's recommendation. Don't brief around them.
3. **Core plan.** Slice the core batch into small slices. For each slice give its ACs, its scenario ids, the files it touches in each repo, its definition of done and its order. Fable reviews the plan. Then show me the plan, Fable's verdict and the defaults list. Build only after I approve.
4. **Build.** Before any change to a file that already exists, show me the diff in chat and apply it only after I approve. New files are built freely. Brief one Sonnet engineer per slice. Only one engineer edits a repo at a time; read-only jobs may run in parallel. A slice is done when:
   - each scenario under its ACs is a passing test;
   - its results agree with the test oracle;
   - new code has tests that run here, and any test that can't run here is written and listed as "not runnable here";
   - the handover doc records anything added beside someone else's code;
   - no one else's file was edited, except the ones I approved in step 1.
5. **Reviews.** Run the two loops from the skill:
   - When Sonnet has finished several slices, you audit them. Give feedback and ask questions until every slice passes.
   - When you have finished a set of those batches, bring it to Fable. Fable audits your work, gives feedback and asks questions, and you loop with it until it accepts the set.

   Bring me every judgment call, two at a time. Call Fable whenever you are stuck or a call is high-stakes.
6. **Epic end.** A fresh Fable does a cold review of the whole epic. Then give me:
   - the diff of every existing-file change;
   - a summary of the new files;
   - the test commands and their output;
   - Fable's verdict;
   - the open findings and the decisions waiting.

   I review and commit. Then start the next epic.
7. **Next batch.** Repeat steps 3 to 6 for the remaining epics. Re-run the inventory first if the core batch changed it.

Use subagents, not an agent team. Propose a workflow only for a large fan-out audit, such as one checker per AC at epic end, and give me its rough cost. It runs only if I opt in. Stop for me only at: the inventory report, each blocker pair, the core plan, each change to an existing file, judgment calls two at a time, and the end of each epic. Never end a turn with a summary that announces the next step, an offer to continue, or a list of non-blocking decisions. Put status in the same message as your next action. Show status against the epics, and the slices in the current epic, at every round.
