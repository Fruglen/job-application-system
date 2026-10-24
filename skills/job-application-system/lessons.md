# Lessons log

This log is what makes the system better and better. Every mistake
the system makes, and every correction the human gives, becomes a
standing rule here the same day. A mistake is allowed. Repeating
one is not.

## Format

Every entry follows this exact shape:

```text
- EXPERIENCE ([DATE], [LANE]): CUE: [the situation that should
  trigger recall] / LESSON: [the rule] / EVIDENCE: [what actually
  happened, with the concrete result] / CONFIDENCE: [high, medium,
  or low, and why].
```

Rules for entries:

- One entry per lesson. No free-form essays, no backfill churn.
- Evidence must be concrete: counts, times, named artifacts, real
  outcomes. A lesson without evidence is a guess, not a lesson.
- Confidence must say why: what confirms it, and what would weaken
  it.
- When a probe adopts a change, the entry names the file the change
  replaced. The winning artifact becomes the live version in the
  same session. No "noted for later" improvements.

## The improvement loop

On any result that misses the standard, do not rerun the same
approach:

1. Pull the live numbers.
2. Study who IS hitting the standard, starting with your own best
   results, then top performers in the lane.
3. Research with the best available models and sources.
4. Change the approach. Probe it against the current one on the
   SAME real task, and compare measured outputs. Verifying that a
   change merely works is not a probe.
5. Adopt the winner in the same session.
6. Record the EXPERIENCE entry the same day.

If the new approach still fails, debug again with a DIFFERENT fix,
never the same one twice.

## Seed lessons

These are the general lessons the framework ships with. Replace the
examples with your own evidence as you run it.

- EXPERIENCE (send timeouts): CUE: an email send call times out or
  its batch is killed mid-run. LESSON: a timeout says NOTHING about
  delivery; the send may complete in the background. Never retry on
  timeout until Sent mail has been checked for that recipient, and
  allow a few minutes for the send to land before concluding it is
  absent. EVIDENCE: in one batch, every reported timeout across two
  rounds had actually delivered, while one clean authentication
  failure genuinely had not sent and succeeded on retry. Final
  state: all sends delivered, zero duplicates, all read-back
  verified. CONFIDENCE: high, timeouts and clean failures behaved
  differently and consistently.

- EXPERIENCE (duplicate sends): CUE: a recruiter reply exists as a
  draft while any sweep or watch also owns that thread. LESSON:
  before sending, check Sent and Drafts for the thread in the same
  pass; if a send is already verified in Sent, trash the draft and
  send nothing. EVIDENCE: a recruiter received two verified sends
  minutes apart (one with a tailored resume, one with the canonical
  resume) after a killed send attempt hid the first outcome; the
  stale draft had been trashed before the second send and still
  duplicated. CONFIDENCE: high, both sends were read back from Sent
  directly.

- EXPERIENCE (brief anchors go stale): CUE: briefing a worker with
  anchors from a previous filing session. LESSON: after any session
  that files submissions, re-derive brief anchors from a FRESH
  registry run (count plus first plus last), never carry the
  previous brief's anchors forward. Also instruct "count non-empty
  lines": a blank line between pasted list blocks inflates naive
  line counts. EVIDENCE: a brief carried a stale count and last
  entry; the true registry output ended with a different entry, and
  the worker correctly stopped with zero filings. CONFIDENCE: high,
  the stale and fresh outputs were compared directly.

- EXPERIENCE (skip bullets parse junk): CUE: writing skip bullets
  with explanatory phrases after semicolons. LESSON: parsers that
  split bullets on separators extract every chunk as a potential
  name, so keep skip bullets to the strict shape with a SHORT reason
  containing no semicolons and no extra company-like noun phrases;
  put detailed reasons in a separate narrative note bullet. After
  writing, re-run the count and grep the skip output for the label
  words used. EVIDENCE: one session's count came in higher than
  expected; three junk fragments from long reasons were found, the
  bullets rephrased, and the count re-verified with all legitimate
  adds present and zero overlap. CONFIDENCE: high, mechanism
  confirmed by before and after runs.

- EXPERIENCE (new marker shapes drop silently): CUE: a track files
  its first submission with a new marker shape. LESSON: verify the
  parser actually picked it up. A clean parse with no warnings can
  still silently drop entries. EVIDENCE: a new marker shape was
  never parsed, one submission was silently dropped, and the count
  stayed flat with no error; patching the parser and diffing the
  live file showed exactly one added entry and zero other diffs.
  CONFIDENCE: high, the diff proved the mechanism.

- EXPERIENCE (state files): CUE: writing any state file (registry,
  ledger, tracker). LESSON: never write a state file in place.
  Write to a new file, verify by parsing it back, then move it into
  place. EVIDENCE: an in-place write truncated a live file when the
  write itself errored, destroying hundreds of prior entries with
  no backup anywhere. CONFIDENCE: high, the failure mode is
  mechanical and repeatable.

- EXPERIENCE (prospect replies are alerts): CUE: a prospect replies
  or books from any outreach. LESSON: a booking or prospect reply
  is a top-priority standalone alert the moment it is detected,
  never folded into a periodic briefing or an audit list. Burial in
  a briefing equals not telling the human. EVIDENCE: a first
  booking from an outreach batch was detected in the morning but
  only surfaced in a briefing; the human found the acceptance
  himself that night and had to ask whether it was a lead.
  CONFIDENCE: high, the human's correction was explicit.

## Growing this log

- Add an entry the same day a lesson is learned. Never batch them
  for later.
- Review the log at the start of each week. Promote repeated
  lessons into SKILL.md rules; delete entries that a newer entry
  has replaced, and note the replacement.
- Keep entries short. A short, accurate log beats a long, stale one.
