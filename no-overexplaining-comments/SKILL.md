---
name: no-overexplaining-comments
description: Cut redundant, over-explaining code comments. Use whenever writing or reviewing code — check that no comment just narrates what the next line obviously does; keep only comments that explain a non-obvious why, a gotcha, or an invariant the code itself can't express. Trigger whenever writing or reviewing code, in any language.
---

# No Overexplaining (code comments)

A comment should tell the reader something the code doesn't already say. It should not narrate what the next line does — a competent reader of the language can already see that.

## The test

Before writing a comment, ask: **if I cut this, would the reader lose anything they couldn't get by just reading the code?**

- If no — cut it.
- If it explains *why* a choice was made, a gotcha, a non-obvious invariant, or a constraint that isn't visible in the code itself — keep it, phrased as tightly as possible.

Don't write a comment just because a line looks complex at a glance; if it's genuinely hard to follow, the better fix is usually clearer naming or a smaller function, not a caption explaining what it does.

## Examples

- Bad: `// increment the counter` above `count += 1`
- Bad: `// loop through the list of users` above `for user in users:`
- Bad: `// return the result` above `return result`
- Bad: `// check if the user is an admin` above `if user.is_admin:`
- Fine: `// retry once — the upstream API flakes under load` above a retry block
- Fine: `// deliberately not using the cached value here, see #4821`
- Fine: `// order matters: must run before the migration below` above a setup step
- Fine: `// O(n) not O(n log n) — profiled faster for our typical n < 50` above a sort-avoiding loop

If a comment just restates the function or variable name in sentence form, delete it — the name is already doing that job.

## A useful check

Read the comment alone, without the code beneath it. If it teaches you something you couldn't have guessed from a well-named function/variable one line below it, keep it. If it's just a translation of the code into English, it's not pulling its weight.
