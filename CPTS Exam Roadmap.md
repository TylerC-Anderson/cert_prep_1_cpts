## CPTS Exam Roadmap

Forward study plan from the post-hiatus restart to CPTS-exam-ready. Grounded in live HTB account progress (re-verified 2026-08-17), not the stale diary checkboxes.

> 📚 **Resources:** [[HTB Platform & Resources]] — HTB's own offerings (what's current vs retired) + vetted external practice/learning, status-checked.

### Where I am (verified from HTB account, 2026-08-17)

- **Path:** Penetration Tester (id 16) — **1 of 28 modules fully done.**
- ✅ **Penetration Testing Process** (id 90) — 15/15 sections.
- 🔶 **Getting Started** (id 77) — 11/23 sections (done through *Privilege Escalation*; *Transferring Files* → *Knowledge Check* remain, ~4h).
- ⬜ 26 modules untouched.
- **Remaining effort: ~330 content-hours** (HTB's own per-module estimates, which run generous).

### The plan: hybrid pace with a calibration checkpoint

Target is **done by December**, hoped capacity **~10 hrs/week**. Those don't both fit the full path — at 10 hrs/week, ~330h lands the exam around **March 2027**. To content-complete by end-November (leaving December for the exam) needs a sustained **~19–22 hrs/week**.

So: **start at ~10 hrs/week, calibrate a personal pace multiplier over the first 3 modules (weeks 34–36), then re-forecast at the checkpoint and decide whether to ramp toward December or accept a later date.** HTB's estimates likely overshoot for someone with PJPT — the calibration tells us by how much, with real data instead of a guess.

### Calibration window (weeks 34–36, Aug 17 – Sep 6)

Detailed week files: `1_Diary/0_Weeks/Calweek-2026-34.md` → `Calweek-2026-36.md`. Gamified version: `CPTS RPG Progression Tree.md` (calibration arc).

| Week | Dates | Module(s) | HTB est | Track your actual hrs |
|------|-------|-----------|---------|-----------------------|
| 34 | Aug 17–23 | Getting Started (finish) + Network Enumeration with Nmap | ~11h (4 + 7) | ___ |
| 35 | Aug 24–30 | Footprinting (part 1) | ~10h of 16h | ___ |
| 36 | Aug 31 – Sep 6 | Footprinting (finish) → **CHECKPOINT** | ~6h | ___ |

**At the week-36 checkpoint:** sum actual hours vs HTB's ~27h estimate for these three modules → that ratio is your personal multiplier. Multiply the remaining ~300h by it, divide by your sustainable weekly hours, and that's the honest exam date. Decide then: hold 10h (later date) or ramp (December).

### Full module sequence (HTB's curated order; hours are HTB estimates)

Cumulative assumes the ~330h remaining. "Wk @10h" = target week if you held exactly 10 hrs/week from week 34 — **provisional past the checkpoint**, to be re-forecast.

| # | Module | id | HTB hrs | Cum | Wk @10h | Thin-note rebuild trigger |
|---|--------|----|---------|-----|---------|---------------------------|
| 1 | Penetration Testing Process | 90 | — | — | ✅ done | — |
| 2 | Getting Started (remainder) | 77 | 4 | 4 | 34 | — |
| 3 | Network Enumeration with Nmap | 19 | 7 | 11 | 34 | — |
| 4 | Footprinting | 112 | 16 | 27 | 35–36 | `Enumerating SSH` |
| 5 | Information Gathering - Web | 144 | 8 | 35 | 37 | `Website Reconnaissance`✓ |
| 6 | Vulnerability Assessment | 108 | 2 | 37 | 37 | — |
| 7 | File Transfers | 24 | 3 | 40 | 38 | — |
| 8 | Shells & Payloads | 115 | 16 | 56 | 38–40 | `Web Shell`, `Upgrade shell to a TTY` |
| 9 | Using the Metasploit Framework | 39 | 5 | 61 | 40 | `Metasploit`✓ |
| 10 | Password Attacks | 147 | 8 | 69 | 41 | `Hashcracking` |
| 11 | Attacking Common Services | 116 | 8 | 77 | 42 | — |
| 12 | Pivoting, Tunneling & Port Forwarding | 158 | 16 | 93 | 43–44 | `Pivoting`, `Lateral Movement in General` |
| 13 | **Active Directory Enumeration & Attacks** | 143 | **56** | 149 | 45–50 | `Attacking AD`, `Pingcastle`, `Ldapdomaindump`, `Bloodhound and Plumhound`, `Mimikatz`, `NTDS.dit` |
| 14 | Using Web Proxies | 110 | 8 | 157 | 51 | `Burp Suite`✓ |
| 15 | Attacking Web Applications with Ffuf | 54 | 5 | 162 | 51 | — |
| 16 | Login Brute Forcing | 57 | 6 | 168 | 52 | — |
| 17 | SQL Injection Fundamentals | 33 | 8 | 176 | 53 | `Exploiting SQL - SQLi` |
| 18 | SQLMap Essentials | 58 | 8 | 184 | 54 | — |
| 19 | Cross-Site Scripting (XSS) | 103 | 6 | 190 | 55 | `XSS - Cross Site Scripting` |
| 20 | File Inclusion | 23 | 8 | 198 | 56 | — |
| 21 | File Upload Attacks | 136 | 8 | 206 | 57 | — |
| 22 | Command Injections | 109 | 6 | 212 | 58 | `Command Injection` (empty — rebuild) |
| 23 | Web Attacks | 134 | 16 | 228 | 59–60 | — |
| 24 | Attacking Common Applications | 113 | 32 | 260 | 61–63 | — |
| 25 | Linux Privilege Escalation | 51 | 8 | 268 | 64 | `GTFO Bins`, `LinPEAS/WinPEAS`✓ |
| 26 | Windows Privilege Escalation | 67 | 32 | 300 | 65–67 | — |
| 27 | Documentation & Reporting | 162 | 16 | 316 | 68–69 | `Reporting` |
| 28 | Attacking Enterprise Networks (capstone) | 163 | 14 | 330 | 70 | — |

(✓ = thin note already covered/healthy or minor; no rebuild needed.)

**The three monsters** — AD (56h), Attacking Common Applications (32h), Windows PrivEsc (32h) — are 120h, over a third of the path. AD is also the single most exam-critical module. Any ramp decision should protect full time on these.

### Note-taking & reinforcement

- **Pace assumption:** ~PJPT baseline — AI tooling speeds notes, but denser text-only material offsets it (a wash) until calibration data says otherwise. No mandated per-section note; note what you'll need to reference later.
- **Reinforcement is mostly free:** the thin notes rebuild as a byproduct when you reach their trigger module (right column above), using the `lesson-to-notes` skill.
- **Immediate housekeeping (do anytime):**
  - Delete `3_Exploitation/Post-Compromise Exploitation/Untitled.md` (0-byte orphan).
  - `3_Exploitation/Command Injection.md` is 0 bytes — rebuild at module 109, or delete now.
- **Manual/no-source thin notes** (hand-author when convenient, not module-triggered): `General IT Tools`, `GTFO Bins`, `0_General - Enumeration Gathering`, `Lateral Movement in General`, `Post-Exploitation in General`, `Persistence & Maintaining Access`.

### Pre-exam (after path content)

CPTS is a hands-on, report-graded exam (10-day window). Reserve **~2 weeks** after the path:
1. A full mock pentest on a retired multi-machine box / Pro Lab (module 163 *Attacking Enterprise Networks* is the built-in capstone rehearsal).
2. A report dry-run using the *Documentation & Reporting* deliverable format.
3. Only then book the exam window.

### Decision log

- **2026-08-15** — Framing: *hybrid — ~10h/week now, calibrate over the first 3 modules (Getting Started, Nmap, Footprinting), re-forecast at the checkpoint*. Target December, but December-vs-10h-vs-full-path is a pick-two; the checkpoint resolves it with real data.
- **2026-08-17** — Calibration begins week 34: Getting Started (finish) and Network Enumeration with Nmap share this week (~11h); Footprinting spans weeks 35–36 to the checkpoint. A true calibrating run — log actual hours each week; the week-36 checkpoint math turns them into the pace multiplier and the exam date.
