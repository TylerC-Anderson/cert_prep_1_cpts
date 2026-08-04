## CPTS Exam Roadmap

Forward study plan from the post-hiatus restart (2026-08-03) to CPTS-exam-ready. Built on live HTB
account progress pulled 2026-08-03, not the stale diary checkboxes.

### Where I am (verified from HTB account, 2026-08-03)

- **Path:** Penetration Tester (id 16) — **5.3% complete, 1 of 28 modules done.**
- ✅ **Penetration Testing Process** (id 90) — 15/15 sections.
- 🔶 **Getting Started** (id 77) — 11/23 sections (done through *Privilege Escalation*; *Transferring Files* → *Knowledge Check* remain, ~4h).
- ⬜ 26 modules untouched.
- **Remaining effort: ~330 content-hours** (HTB's own per-module estimates, which run generous).

### The plan: hybrid pace with a calibration checkpoint

Target is **done by December**, hoped capacity **~10 hrs/week**. Those don't both fit the full path —
at 10 hrs/week, ~330h lands the exam around **March 2027**. To content-complete by end-November (leaving
December for the exam) needs a sustained **~19–22 hrs/week**.

So: **start at 10 hrs/week, calibrate a personal pace multiplier over the first 3 modules (weeks 32–35),
then re-forecast at the checkpoint and decide whether to ramp toward December or accept a later date.**
HTB's estimates likely overshoot for someone with PJPT — the calibration tells us by how much, with real
data instead of a guess.

### Calibration window (weeks 32–35, Aug 3 – Aug 30)

Detailed week files: `1_Diary/0_Weeks/Calweek-2026-32.md` → `Calweek-2026-35.md`.

| Week | Dates | Module(s) | HTB est | Track your actual hrs |
|------|-------|-----------|---------|-----------------------|
| 32 | Aug 3–9 | Getting Started (finish) | ~4h | ___ |
| 33 | Aug 10–16 | Network Enumeration with Nmap | 7h | ___ |
| 34 | Aug 17–23 | Footprinting (part 1) | ~10h of 16h | ___ |
| 35 | Aug 24–30 | Footprinting (finish) → **CHECKPOINT** | ~6h | ___ |

**At the week-35 checkpoint:** sum actual hours vs HTB's ~27h estimate for these three modules → that ratio
is your personal multiplier. Multiply the remaining ~300h by it, divide by your sustainable weekly hours,
and that's the honest exam date. Decide then: hold 10h (later date) or ramp (December).

### Full module sequence (HTB's curated order; hours are HTB estimates)

Cumulative assumes the ~330h remaining. "Wk @10h" = target week if you held exactly 10 hrs/week from
week 32 — **provisional past the checkpoint**, to be re-forecast.

| # | Module | id | HTB hrs | Cum | Wk @10h | Thin-note rebuild trigger |
|---|--------|----|---------|-----|---------|---------------------------|
| 1 | Penetration Testing Process | 90 | — | — | ✅ done | — |
| 2 | Getting Started (remainder) | 77 | 4 | 4 | 32 | — |
| 3 | Network Enumeration with Nmap | 19 | 7 | 11 | 33 | — |
| 4 | Footprinting | 112 | 16 | 27 | 34–35 | `Enumerating SSH` |
| 5 | Information Gathering - Web | 144 | 8 | 35 | 36 | `Website Reconnaissance`✓ |
| 6 | Vulnerability Assessment | 108 | 2 | 37 | 36 | — |
| 7 | File Transfers | 24 | 3 | 40 | 37 | — |
| 8 | Shells & Payloads | 115 | 16 | 56 | 37–39 | `Web Shell`, `Upgrade shell to a TTY` |
| 9 | Using the Metasploit Framework | 39 | 5 | 61 | 39 | `Metasploit`✓ |
| 10 | Password Attacks | 147 | 8 | 69 | 40 | `Hashcracking` |
| 11 | Attacking Common Services | 116 | 8 | 77 | 41 | — |
| 12 | Pivoting, Tunneling & Port Forwarding | 158 | 16 | 93 | 42–43 | `Pivoting`, `Lateral Movement in General` |
| 13 | **Active Directory Enumeration & Attacks** | 143 | **56** | 149 | 44–49 | `Attacking AD`, `Pingcastle`, `Ldapdomaindump`, `Bloodhound and Plumhound`, `Mimikatz`, `NTDS.dit` |
| 14 | Using Web Proxies | 110 | 8 | 157 | 50 | `Burp Suite`✓ |
| 15 | Attacking Web Applications with Ffuf | 54 | 5 | 162 | 50 | — |
| 16 | Login Brute Forcing | 57 | 6 | 168 | 51 | — |
| 17 | SQL Injection Fundamentals | 33 | 8 | 176 | 52 | `Exploiting SQL - SQLi` |
| 18 | SQLMap Essentials | 58 | 8 | 184 | 53 | — |
| 19 | Cross-Site Scripting (XSS) | 103 | 6 | 190 | 54 | `XSS - Cross Site Scripting` |
| 20 | File Inclusion | 23 | 8 | 198 | 55 | — |
| 21 | File Upload Attacks | 136 | 8 | 206 | 56 | — |
| 22 | Command Injections | 109 | 6 | 212 | 57 | `Command Injection` (empty — rebuild) |
| 23 | Web Attacks | 134 | 16 | 228 | 58–59 | — |
| 24 | Attacking Common Applications | 113 | 32 | 260 | 60–62 | — |
| 25 | Linux Privilege Escalation | 51 | 8 | 268 | 63 | `GTFO Bins`, `LinPEAS/WinPEAS`✓ |
| 26 | Windows Privilege Escalation | 67 | 32 | 300 | 64–66 | — |
| 27 | Documentation & Reporting | 162 | 16 | 316 | 67–68 | `Reporting` |
| 28 | Attacking Enterprise Networks (capstone) | 163 | 14 | 330 | 69 | — |

(✓ = thin note already covered/healthy or minor; no rebuild needed.)

**The three monsters** — AD (56h), Attacking Common Applications (32h), Windows PrivEsc (32h) — are 120h,
over a third of the path. AD is also the single most exam-critical module. Any ramp decision should protect
full time on these.

### Note-taking & reinforcement

- **Pace assumption:** ~PJPT baseline — AI tooling speeds notes, but denser text-only material offsets it (a
  wash) until calibration data says otherwise. No mandated per-section note; note what you'll need to
  reference later.
- **Reinforcement is mostly free:** the thin notes rebuild as a byproduct when you reach their trigger
  module (right column above), using the `lesson-to-notes` skill.
- **Immediate housekeeping (do anytime):**
  - Delete `3_Exploitation/Post-Compromise Exploitation/Untitled.md` (0-byte orphan).
  - `3_Exploitation/Command Injection.md` is 0 bytes — rebuild at module 109, or delete now.
- **Manual/no-source thin notes** (hand-author when convenient, not module-triggered): `General IT Tools`,
  `GTFO Bins`, `0_General - Enumeration Gathering`, `Lateral Movement in General`, `Post-Exploitation in General`,
  `Persistence & Maintaining Access`.

### Pre-exam (after path content)

CPTS is a hands-on, report-graded exam (10-day window). Reserve **~2 weeks** after the path:
1. A full mock pentest on a retired multi-machine box / Pro Lab (module 163 *Attacking Enterprise Networks*
   is the built-in capstone rehearsal).
2. A report dry-run using the *Documentation & Reporting* deliverable format.
3. Only then book the exam window.

### Decision log

- **2026-08-03** — Framing set to *hybrid: 10h now, calibrate over first 3 modules, re-forecast at week 35*.
  Target December, but December-vs-10h-vs-full-path is a pick-two; the checkpoint resolves it with real data.
