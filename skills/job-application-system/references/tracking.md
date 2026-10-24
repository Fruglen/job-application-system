# Registry and tracking

The registry is the campaign's source of truth. It holds two lists
per track: submitted and skipped. Every session reads it first and
reconciles it last.

## File layout

One registry file per campaign. Each track has its own sections:

```text
## [TRACK NAME] submitted
- [TRACK ABBR] #[NUMBER]: [Company] - [Role] - [Location/remote] - [Route] - [Confirmation or note]

## [TRACK NAME] skipped
- [Company] - [Role]: [short reason]
```

## Numbering

- Each track counts separately, starting from its own first number.
- A number is consumed only by a verified submission. Blocked
  attempts (CAPTCHA loop, page removed, sign-in lost, identity
  unverified) never consume a number.
- A reserved or on-hold number is never renumbered. The sequence
  keeps its gaps; gaps are history, not errors.

## Anchors

After any session that files submissions, re-derive the brief
anchors from a FRESH registry run before the next session:

- Total submitted count.
- First submitted entry.
- Last submitted entry.

Never carry the previous session's anchors forward. A stale anchor
can make a worker stop early or file duplicates.

Count non-empty lines only. A blank line between pasted list blocks
inflates naive line counts.

## Count reconciliation

After every session, verify:

- Submitted count plus skipped count equals the expected totals.
- Zero overlap between the submitted list and the skipped list.
- Every new submission appears in the submitted list, and every new
  skip appears in the skipped list.

If the counts do not reconcile, stop. Do not move the file into
place, do not start the next session, and find the missing entry
first.

## Skip bullet rules

Skip entries must parse cleanly. Use exactly one of these two
shapes, and nothing else:

Shape 1, the "(not pursued)" bullet:

```text
- [Company] - [Role] (not pursued): [short reason]
```

Shape 2, the same-line encounters bullet:

```text
- Skip-list encounters avoided: [Company], [Company], [Company]
```

Rules for both shapes:

- Reasons are SHORT. No semicolons. No extra company-like noun
  phrases in the reason.
- Put detailed reasons in a separate narrative note bullet. Note
  bullets are not parsed the same way as skip bullets.
- After writing new skip bullets, re-run the count and grep the
  skip output for the label words used in the new bullets. Junk
  fragments (phrases split out of a long reason) must be caught
  here, not discovered later.
- Ultra-short names that a parser may drop are left out of the
  skip list and noted as re-screen on next encounter. Never
  force-file a name the parser cannot hold.

## Parser checks

- After any track's first-ever submission of a new marker shape
  (a new track tag, a new confirmation format), verify the parser
  actually picked it up. A clean parse with no warnings can still
  silently drop entries.
- If a count stays flat after a session that filed submissions,
  the parser missed something. Diff the registry before and after
  to find exactly what changed.

## Briefs to workers

- Briefs always go inline in the task text, never as a file grant.
  Granted files arrive as upload inputs only and cannot be read as
  brief text.
- A tightened brief that omits the skip list is UNSAFE unless the
  session uses interactive pre-submission verification: the worker
  checks each candidate against the live skip list before filing,
  and the human confirms.
