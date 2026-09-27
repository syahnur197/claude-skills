---
name: no-overexplaining-ui
description: Cut redundant, over-explaining wording in UI copy and in Claude's own conversational replies. Use whenever writing or reviewing UI strings (empty states, tooltips, banners, disclaimers, placeholders, option/settings descriptions) or any reply to the user — check that nothing states the obvious, spells out what a reader would already infer, leaks internal business/permission logic into user-facing text, sits as permanent inline text when it should be behind a tooltip/FAQ instead, restates a self-evident heading, or cites sources for low-stakes content nobody's questioning. Trigger on requests to design/write UI or just chat normally.
---

# No Overexplaining (UI & conversation)

Most readers can infer the obvious from context. Text that spells it out anyway isn't helpful — it's noise they have to read past to get to the part that matters. This applies to UI copy and to how Claude talks in a normal reply.

## The test

Before writing a line of copy or a sentence in a reply, ask: **if I cut this, would the reader lose anything they couldn't already tell?**

- If no — cut it.
- If it adds real information (why something happened, what to do next, a non-obvious constraint) — keep it, but say it in as few words as possible.

Don't pad a short, sufficient line into a longer one to sound more complete or more polished. Length is not a sign of thoroughness; it's usually a sign the obvious got restated.

## UI copy

Empty states, tooltips, banners, and placeholders tend to accumulate explanation nobody asked for, because it feels safer to spell things out. Resist that.

- A short label is usually enough on its own. "No messages yet" doesn't need a follow-up sentence explaining what a message is or how the inbox will populate — the reader is looking at an "Inbox" screen; they know.
- If a helper line adds something real (e.g., what action unblocks the empty state), keep it — but trim it to the action, not a mini-essay. "When someone replies to a listing, it'll show up here" → just "Nothing here yet" plus a CTA button is often enough; only keep the explanatory clause if the mechanism is genuinely non-obvious.
- Never add a caveat/disclaimer badge or label unless the user asked for one or it's load-bearing (e.g., real legal/safety requirement). A "Beta — content may be inaccurate" style badge on every screen of an app is clutter unless someone specifically needs that disclaimer there.
- Avoid the "X will happen if Y happens" construction as a default — it's almost always spelling out something the UI already makes obvious through layout, icon, or heading.
- If the heading already states the purpose ("Track your package."), don't follow it with a paragraph restating the mechanism (what a tracking number is, how couriers use it, why you'd look one up). A visitor who landed on a package tracker already knows what tracking a package does — that's why they're there.
- Don't cite a source/reference for low-stakes, self-evidently-correct content. A citation like "Source: National Postal Authority, Address Format Handbook, 3rd ed." makes sense on a page where the *authority* of the data is in question (a disputed figure, a legal or medical claim) — not on a simple address-format checker, where the tool either validates correctly or it doesn't, and no one is going to go verify it against the source handbook. If the content isn't the kind of thing a reader would want to interrogate, don't hand them a citation for it; it just adds authority-flavored clutter to something nobody doubted.

**Before / after:**
- Before: "You haven't posted a listing yet. 12 categories are open right now. Your listings and their views will show here."
- After: "No listings yet." (the CTA button "Create a listing" already tells them what to do)

- Before: "No messages yet. When a buyer contacts you about an item, the conversation shows here."
- After: "No messages yet."

- Before: "No offers yet · most listings get one within a day — try adding more photos or lowering the price"
- After: "No offers yet" (drop the speculative advice unless it's genuinely actionable and specific, not generic filler)

### Don't over-explain the "why" behind data the user's own action already explains

A common form of this: the user takes an action that implies where data came from and what to do about it, and the UI spells that out anyway — leaking backend/business logic the user never asked about.

Example: a user verifies their identity through a government digital-ID login, which prefills their profile fields. The user *chose* that login flow specifically to get their info prefilled — they already know where it came from and where to fix it if it's wrong. A line like "Your details are pulled from your government ID; if anything is outdated, update it with the issuing authority" tells them nothing they didn't infer the moment they picked that login option.

Ask: did the user do something that already implies this fact? If yes, restating it is exposing internal logic as if it were news. Only surface the source/mechanism when it's genuinely not inferable from what the user just did (e.g., data appeared without the user taking an action tied to that source).

### Don't let internal implementation/permission logic leak verbatim into copy

A second, sneakier form: text that reads like it was copy-pasted straight from how the feature was *decided* or *built*, rather than written for what the reader actually needs to know.

This tends to happen when a feature starts life as an internal instruction — a prompt, a ticket, a permission check — phrased as a business rule ("allow X regardless of plan tier", "only show Y if the user is verified", "enable Z after 3 failed attempts"). When that instruction gets implemented, the condition it describes sometimes gets echoed directly into the UI as if it were information the user needs, instead of being translated into what actually matters to them (often: nothing at all, because the condition already resolved in their favor).

Example: a profile-photo upload field shows "Available on every plan." No one asked about plan tiers — they came to upload a photo. Somewhere upstream, someone likely instructed "let's allow all users to set a profile photo regardless of their plan," and that internal permission decision got surfaced as reassurance nobody needed. If a feature is available, the UI for it just... being present and usable is the message. Announcing eligibility is only useful when eligibility is genuinely in question (e.g., a feature that IS gated, shown to a user who ISN'T eligible, with an upgrade path) — not as a blanket reassurance on a feature everyone gets anyway.

The tell: if a sentence's only content is describing a rule, condition, or permission state rather than helping the reader do something, ask whether that rule is actually in doubt for this reader right now. If it isn't, the sentence is an artifact of how the feature was built, not something the reader needed to see — cut it.

### Non-obvious doesn't mean it belongs inline

Being genuinely useful and non-obvious is the bar for keeping information at all — it is not, by itself, a reason to print it as permanent body text under every option on the screen. A screen with several choices, each with a paragraph of caveats sitting always-visible beneath it, is cluttered even when every sentence individually passes the "is this obvious" test. Most people scanning the screen don't need that detail to make the choice; a few people occasionally do.

So split the question in two:
1. Is this true and useful to someone? (the earlier tests in this doc answer that)
2. Does the reader need it **right now, to make the decision in front of them** — or would they only want it if they went looking?

If the answer to (2) is "only if they went looking," the detail belongs behind a tooltip, an info icon, an expandable "Learn more," or a FAQ/help link — not inline. Reserve permanent inline text for the few facts that would change what a reasonable person decides in that moment (e.g., a cost, a destructive/irreversible action, a hard eligibility block). Everything else — mechanics, edge cases, "what happens if," background on how a feature works — is progressive disclosure material: available on demand, invisible by default.

**Example:** a rewards-program settings screen with two mode cards. "Points are calculated nightly, not in real time" and "Turning rewards off stops new points from accruing; existing balances stay preserved" are both accurate and non-obvious — but neither changes which of the two modes someone picks up front. Printed inline under every card, on every visit, for every account, they're clutter multiplied by frequency. They belong behind a ⓘ next to the toggle, not as standing paragraphs.

## Conversational replies

Same instinct applies to how Claude talks, not just what it writes into UI. Don't:
- Restate the user's question before answering it
- Explain a mechanism the user clearly already understands from how they asked
- Pad a short factual answer with throat-clearing or a recap of what was just said
- Add a qualifying sentence that just hedges without adding new information

If a one-line answer is a complete answer, give the one line. Add more only when there's a real next fact, trade-off, or caveat to convey.
