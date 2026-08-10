# Customer Meeting Calendar Automation

An automated pipeline that detects customer meetings across the team's Google Calendars, logs each one to a Notion database with full metadata, and attaches the meeting's recording, transcript, and AI summary — turning a manual, person-dependent process into a hands-off, always-current record of every customer interaction.

> Built during my summer 2026 internship at **Chezie**. Public repo is scrubbed of credentials and real customer data.


---

## What it is
A scheduled automation that:
1. **Detects customer meetings** on four team members' Google Calendars automatically.
2. **Creates a Notion page** for each detected meeting, pre-populated with title, date/time, attendees, platform (Zoom/Meet), and the owning team member.
3. **Identifies which meetings are customer meetings** by matching attendee email domains against the list of active customers.
4. **Captures artifacts after the meeting** — pulls the recording URL, transcript, and auto-summary from the team's note-taking tools and writes them into the page (summary on top, transcript in the body).

## Why it was needed (the problem)
Customer meeting records were created **by hand** by the EA, who monitored four separate calendars (Toby, Dumebi, Kate, Jesse) and manually built a Notion page per meeting. It was time-consuming, easy to miss meetings, dependent entirely on one person's bandwidth, and captured no transcripts — so there was no reliable, AI-readable history of interactions with any given customer.

## What I built / how it works
- **Calendar monitoring** across all four team members' Google Calendars, checked automatically at least once a day (OAuth app via Google Cloud Console).
- **Customer-detection logic** that matches attendee email domains against the ~25 active (non-churned) customers in the Renewals Tracker, so only real customer meetings get logged.
- **Automated Notion page creation** via the Notion API, pre-filled with meeting metadata, plus **duplicate detection** (keying on the meeting ID) so re-runs never create repeats.
- **Artifact ingestion** from the team's note-taking tools (Granola / Fathom) — recording URL, transcript, and the tool's own summary — written into each page; fields left blank gracefully when an artifact isn't available.
- Runs on a schedule with **no manual trigger**.

I approached it product-first: interviewed the four stakeholders, audited the existing Notion databases, wrote and got sign-off on a requirements doc, mapped the data flow, then built and tested against real past meetings.

## Tools & tech
`Google Calendar API` · `Notion API` · `Google Cloud Console (OAuth)` · `Granola / Fathom APIs` · scheduled job · built with `Claude / Claude Code`

## Results / impact
- Eliminated the EA's manual meeting-logging entirely — the system runs on its own.
- Produced a **centralized, AI-readable record** of customer interactions (metadata + transcript + summary) any teammate or AI agent can query.
- Demonstrated end-to-end with real customer meetings correctly detected and logged.
- Weekly average of 23 meetings logged and entered
- Reduces manual work by **5.75 hours per week**.
