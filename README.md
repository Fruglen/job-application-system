# Job Application System

A complete, self-improving skill for running a job search as an operation:
discover roles, verify eligibility, apply across job boards and company
sites, reply to recruiters with tailored resumes, prep for interviews,
and follow up warm threads until offers land.

One skill, one lane: applications. Nothing else lives here.

## What it covers

- Multi-track campaigns (a primary track plus interim-income tracks),
  each with its own number sequence, resume, email, and LinkedIn identity.
- Discovery across company career sites, LinkedIn, Indeed, Monster,
  Dice, and remote boards, with a strict 24-hour freshness rule.
- A registry that tracks every submission and every skip, with counts
  reconciled after every session.
- A recruiter-reply autopilot: any recruiter message gets a JD-tailored
  reply with a tailored resume and a full kit, without per-reply approval.
- LinkedIn outreach in a natural human voice, plus an inbox watch.
- Interview prep for every scheduled interview, and a follow-up system
  that keeps every warm thread alive.
- A lessons loop that makes the system better after every mistake.

## What it never does

- Never invents employers, dates, metrics, certifications, KPIs, or
  anecdotes. Anything without a truthful answer is held and surfaced.
- Never sends ID documents or signs RTR (right-to-represent) agreements
  without the human's explicit decision.
- Never names a salary or rate the human has not discussed.
- Never tells one recruiter that another pitched the same role.
- Never signs out of a job-board session once signed in.

## Install

Clone this repo, then copy the skill into your agent's skills directory:

```text
git clone https://github.com/Fruglen/job-application-system.git
cp -r job-application-system/skills/job-application-system <your-skills-dir>/
```

Then work through [SETUP.md](SETUP.md) before the first run. Every
placeholder in brackets must be filled with your own information. The
skill ships with zero personal data: no names, phones, addresses,
salaries, or account details. Your values stay in your private setup,
never in the shared skill.

## Layout

```text
skills/job-application-system/
  SKILL.md                  The framework. Start here.
  references/
    platforms.md            Platform playbooks (LinkedIn, Indeed, Monster, Dice, company sites, remote boards)
    tracking.md             Registry format, numbering, and parser rules
    recruiter-kit.md        The reply kit, hold rules, and send verification
  templates/
    recruiter-reply.md      Recruiter reply template
    linkedin-dm.md          LinkedIn DM template
    interview-prep.md       Interview prep template
  lessons.md                Lessons log (EXPERIENCE format) and how to grow it
```

## License

MIT. Use it, fork it, improve it, share it.
