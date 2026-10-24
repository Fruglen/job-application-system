---
name: job-application-system
description: Run a complete job-search application operation end to end. Use when the user wants to apply to jobs, run an application campaign, reach recruiters, reply to recruiter messages, prep for interviews, or follow up warm threads. Covers discovery, eligibility verification, applications across job boards and company sites, recruiter autopilot, LinkedIn outreach, interview prep, and follow-up, with a self-improving lessons loop.
---

# Job Application System

A complete application-side framework. One lane: getting hired.
Discovery, application, recruiter handling, interviews, follow-up.
Nothing else lives here.

## Operating contract

The agent runs the work end to end. The human is involved only for:

- Approvals, batched once per wave, not per item.
- Sign-ins, taps, in-app actions, and bookings.
- Facts only the human knows.
- RTR signatures and ID documents (always held, never autopilot).
- Credentials, via a secure flow only.

Report submitted applications one line each. Never send "this job
exists" alerts. Surface only: questions with no truthful answer,
human-hands tasks, and credentials. Everything else, just do it.

## 1. Tracks

A track is one job family with its own identity and counter.

- Each track has its own number sequence, resume, email, and LinkedIn
  profile. Never mix track identities: never send one track's resume
  or LinkedIn URL on another track's application or reply.
- A primary track and any interim-income tracks run in parallel.
- Blocked attempts never consume a track number. A number is consumed
  only by a verified submission.

## 2. Discovery

Routes, in order of use:

- Company career sites (direct applications).
- LinkedIn, Indeed, Monster, Dice.
- Remote boards: We Work Remotely, Wellfound, Hiring Cafe.

See `references/platforms.md` for the playbook per route.

Rules:

- Start every session with the Indeed digest.
- 24-hour freshness rule: apply only to roles posted within the last
  24 hours. Older postings are skipped even if eligible. Never
  re-touch a skip-listed company to hit freshness.
- Warm leads first: follow-ups, live threads, and referrals come
  before cold applications, every session.

## 3. Eligibility gates

Before any application, verify:

- The company is not on the skip list (see `references/tracking.md`).
- Geography fits: the human's home metro, or remote within the
  approved region.
- The role fits the track. Weak fits get an honest reply or a skip,
  never a padded application.
- Salary rules per track (from setup): the primary track states its
  target proactively in recruiter replies and has no floor; other
  tracks never name a fixed number and work within the budgeted range.
- Never name a salary or rate the human has not discussed.

## 4. Applying

- Fill ALL questions on every form. No skipped fields, no
  SmartApply-style shortcut that skips questions.
- Standing answers come from the setup table only: truthful values,
  per-skill years stated separately, never compressed into one
  sentence. Start date, relocation, travel, references, education,
  and work authorization wording are fixed values, not inventions.
- Never invent employers, dates, metrics, certifications, KPIs, or
  anecdotes. Anything without a truthful answer is held and surfaced.
- Never remove the current employer from application history.
- Verification gates are tried once, max, then skip to the next role.
  No parking on a blocked role, no retries, no repeated asks for a
  phone step. A blocked role costs no track number.
- Never sign out of a job-board session once signed in. Preserve
  sessions across runs.
- Portfolio links go on resumes and forms only, never in emails or
  direct messages, unless the setup says otherwise.

## 5. Registry and numbering

See `references/tracking.md` for the full format. The essentials:

- One registry file holds the submitted list and the skipped list
  for every track.
- After any filing session, re-derive brief anchors from a FRESH
  registry run: count, first entry, last entry. Never carry the
  previous session's anchors forward.
- Count non-empty lines only. Blank lines between pasted blocks
  inflate naive counts.
- Reconcile counts after every session: submitted plus skipped, zero
  overlap between the lists.
- Skip bullets use exactly one of two shapes: the "(not pursued)"
  shape, or the "Skip-list encounters avoided:" same-line shape with
  a short reason. No semicolons, no extra company-like noun phrases
  in the reason. Narrative detail goes in a separate note bullet.
- After any track's first-ever submission of a new marker shape,
  verify the parser actually picked it up. A clean parse with no
  warnings can still silently drop entries.

## 6. Resume system: the 20/10 technique

- No "Professional Summary" section.
- A CAREER HIGHLIGHTS section built from bold skill-label lines.
- Every experience bullet opens with a bold skill label plus a colon.
- Labels come from the target posting, ordered by employer priority.
- Career Highlights lines carry no metrics.
- One canonical builder per track; tailored clones trim to one page.
- Verify every resume with a page count check and a rendered page
  image before it goes out. A resume that has not been rendered has
  not been checked.

## 7. Recruiter autopilot

See `references/recruiter-kit.md` for the kit and `templates/` for
the reply text. The rules:

- Any recruiter message, in any inbox, gets read, and a JD-tailored
  reply with a tailored resume and the full kit is SENT without
  per-reply approval.
- HOLD, never autopilot: RTR signatures, ID documents, invented
  facts, and any salary or rate the human has not discussed.
- Reply ONLY to the other party's inbound message, never to the
  human's own sent copy. Corrections to sent mail are fresh sends.
- Before sending, check Sent and Drafts for the thread. If a send is
  already verified in Sent, trash the draft and send nothing.
- Verify the To header and the attachment on EVERY send by reading
  back the saved email.
- A send timeout says NOTHING about delivery. Never retry on a
  timeout or a killed batch until Sent mail has been checked for
  that recipient. Allow a few minutes for the send to land.
- Email bodies containing amounts go through a safe path that
  preserves the amounts exactly; verify amounts on read-back.
- No em dashes in anything sent out.

## 8. Duplicate-role rule

When two recruiters pitch the same role, reply to each independently.
Never tell one recruiter that another pitched the same role. Never
flag a double submission. Let them double-submit; that is the
human's decision, not the agent's warning to deliver.

## 9. Postponement rule

When postponing or rescheduling anything, the reason is ALWAYS "a
family emergency". Never "traveling", never "a family event", never
any other reason.

## 10. LinkedIn outreach

- DM voice: natural warm opener, one genuine observation, one easy
  ask, signed with the first name. Never paste your own LinkedIn URL
  in a LinkedIn DM.
- Watch replies MUST include the profile photo. If the photo cannot
  attach, HOLD the reply, unless the human has waived the photo for
  that specific thread.
- Proactive outreach runs in pilot-sized batches to staffing
  recruiters in the home metro. Measure accepts and replies, and
  re-judge after about a week. Do not scale a batch that has not
  been measured.
- Watch reports can lag. Never claim a clean inbox inside the first
  30 minutes after a run.
- If outbounds appear that no watch run sent, ask the human whether
  they sent them. Do not assume.

## 11. Interviews

- A prep draft is written for EVERY scheduled interview, the moment
  the booking lands: role, company, likely questions, talking
  points, and open items. See `templates/interview-prep.md`.
- Calendar invites are accepted by the human.
- Clash rule: the first party that confirmed keeps the slot. The
  later-confirmed party moves, preferably before the first booking.
- A thank-you goes out after every interview round that took place,
  unless the human says otherwise.
- Log outcomes. An unlogged interview is an open thread, not a
  closed one.

## 12. Follow-ups

- Keep every warm thread alive. A warm thread with no next step is
  a defect.
- Same-week rule: no nudge in the same week as the last touch.
  Move due items to the next week instead of sending early.
- Follow-up timing is per thread, recorded with the thread, and
  checked on a weekly pass.
- Rejections are logged, with the reapply date where one is known.
- A bounced address is never resent to. Dead addresses are dropped
  from the send list.

## 13. State-file safety

- NEVER write a state file in place. Write to a new file, verify by
  parsing it back, then move it into place.
- Never let a transient empty fetch overwrite good state files.
  When a fetch returns nothing, warn and keep the last good state.
- Before repeating any irreversible action whose outcome is
  unknown (a send, a publish, a submission), check the live
  destination first: Sent mail, the live platform, the registry.

## 14. The improvement loop

This is what makes the system better and better. On any result that
misses the standard, do not rerun the same approach:

1. Pull the live numbers.
2. Study who IS hitting the standard, starting with your own best
   results, then top performers in the lane.
3. Research with the best available models and sources.
4. Change the approach. Probe it against the current one on the
   SAME real task, and compare measured outputs. Verifying that a
   change merely works is not a probe.
5. Adopt the winner. The winning artifact becomes the live version
   in the same session. No "noted for later" improvements.
6. Record an EXPERIENCE entry in `lessons.md` the same day, in
   CUE / LESSON / EVIDENCE / CONFIDENCE format, naming the file the
   change replaced. Corrections become standing rules the same day.

Admit mistakes plainly, correct them, and record them. A mistake is
allowed. Repeating one is not.
