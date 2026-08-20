
## About

Living reference of HTB's own offerings + vetted external practice/learning, pulled from *Getting Started* → *Starting Out* (`77:727`) + *Navigating HTB* (`77:731`), and **status-checked Aug 2026** against hackthebox.com + each project's page. The source section is a few years old, so statuses below correct it.

*Guided* (HTB Academy: structured modules) vs *exploratory* (main platform: black-box boxes/challenges). Mix both — structure to learn correctly, exploration to build your own methodology.

Status key: ✅ current · 🟡 alive-but-stale · ⛔ retired/dormant

---

## HTB Platform offerings

| Offering | What it is | Status |
|---|---|---|
| *[Starting Point](https://app.hackthebox.com/starting-point)* | Linear beginner on-ramp (Tier 0–2): VPN → enum → foothold → privesc, then easy boxes | ✅ current |
| *Machines* | Vulnerable boxes, `Easy`→`Insane`; ~1 new + 1 retired each week. Retired go to VIP + official walkthroughs | ✅ current |
| *Challenges* | Bite-size category tasks: web, pwn, crypto, rev, forensics, stego, OSINT, mobile, hardware — plus newer `Blockchain`, `AI-ML`, `GamePwn`, `ICS`, `Coding` | ✅ current |
| *[Tracks](https://app.hackthebox.com/tracks)* | Curated machine+challenge paths on one subject | ✅ current |
| *Fortresses* | Single host with many flags, vendor-sponsored; unlock at Hacker rank | ✅ current |
| *[Pro Labs](https://app.hackthebox.com/prolabs)* | Simulated enterprise networks (mock pentest), now spanning **Red Team Operator Levels I–IV** — from smaller **Mini Pro Labs** (the former Endgames) up to full labs. **Access via VIP+ / Pro Labs Bundle** | ✅ current |
| *Endgames* | Small red-team mini-labs (P.O.O., Hades, Ascension…) | ⛔ **retired as a product** — HTB folded the niche into **Pro Labs** (Oct 2024): *"Former Endgames… are now transitioned to Pro Labs."* They became **Mini Pro Labs** (Ascension, Solar, RPG…) under Red Team Operator Levels |

*Added since this section was written* (not in the source):
- *Seasons* — 13-week competitive mode, everyone starts at zero, one new box/week. Arguably the headline addition.
- *Sherlocks* — blue-team / DFIR investigations (Cloud, malware analysis, SOC, threat intel). VIP-tier.
- *Tier change* — standalone **VIP retired for new purchase (Oct 2025)**; **VIP+** is now the paid consumer tier (free + student tiers remain).
- *Battlegrounds* — ⛔ **retired** (HTB changelog: *"officially retiring Battlegrounds on June 25th"*, most likely 2025 — year not hard-confirmed). **No successor named** for the real-time team-vs-team PvP niche.

---

## Using the platform

*Profile / Rankings*: profile shows your rank, own %, badges, and certs; Rankings pages cover users, teams, universities, and countries.

*Machines — active vs retired*: ~20 active machines at a time; **one new released weekly, one retired the same day** (verified current). Active boxes award ranking points and you solve them blind. Retired boxes give no ranking points but ship official walkthroughs — and need **VIP+** (only the 2 most-recently-retired are free).

*Challenges*: sorted into categories (~10 each), same active/retired split; open a challenge's page to submit its flag.

*Playing a box*: `Join Machine` → you're given its IP → connect over **HTB VPN** to reach it → find and submit the `user` + `root` flags on the machine page. Retired box → the *Walkthroughs* tab (written + video).

*Tracks*: curated machine+challenge paths (beginner → expert); enroll and work through, progress tracked per item.

*Rank gates*: some content is rank-locked — e.g. **Fortresses unlock at `Hacker` rank**. (Endgames were `Guru`-gated, but see the status table — they're retired.)

> ⚠️ This walkthrough section is a few years old (its screenshots still show Endgames, Battlegrounds, and the old VIP tier). Trust the *mechanics* above (the weekly active/retired rotation is verified), but for **what's offered and the tiers, trust the status table above** — not the module's screenshots.

---

## Ranks & XP (two separate systems)

HTB runs **two parallel progression systems** — the module's rank names and the XP blog describe *different* things, which is why "Hacker" never appears in the XP write-up:

- *Legacy Ranks*: Labs-only ladder based on **ownership %** of *active* content. Retired boxes count for nothing, and it's a % of the current pool — so it can **drop** as content retires weekly. This is what gates content like Fortresses.
- *XP / Levels*: a newer, lifetime cumulative score (only goes up, ~100+ levels to Grandmaster) spanning Labs + Academy. Does **not** gate Fortresses.
- *Seasons*: separate short-term competitive sprints.

| Rank | Ownership % | Note |
|---|---|---|
| Noob | 0% | |
| Script Kiddie | >5% | |
| **Hacker** | **>20%** | **unlocks Fortresses** |
| Pro Hacker | >45% | |
| Elite Hacker | >70% | |
| Guru | >90% | (was the Endgames gate) |
| Omniscient | 100% | |

*Reaching Hacker*: exceed 20% on `(ActiveSystemOwns + ActiveUserOwns/2 + ActiveChallengeOwns/10) / (activeMachines + activeMachines/2 + activeChallenges/10) × 100`. Only **active** machines/challenges count; rooting active boxes (system owns weigh fullest) is the fastest route. It's a % of the current pool, so it dips as boxes retire — hold it, don't just hit it once.

---

## Beginner picks (HTB)

*Boxes*: [Lame](https://app.hackthebox.com/machines/1) · [Blue](https://app.hackthebox.com/machines/51) · [Nibbles](https://app.hackthebox.com/machines/121) · [Shocker](https://app.hackthebox.com/machines/108) · [Jerry](https://app.hackthebox.com/machines/144)

*Challenges*: [Find The Easy Pass](https://app.hackthebox.com/challenges/5) · [Weak RSA](https://app.hackthebox.com/challenges/6) · [You know 0xDiablos](https://app.hackthebox.com/challenges/106)

*Pro Lab*: [Dante](https://app.hackthebox.com/prolabs/overview/dante) — still the most beginner-friendly Pro Lab

*IppSec playlists*: [Easy Linux boxes](https://www.youtube.com/playlist?list=PLidcsTyj9JXJfpkDrttTdk1MNT6CDwVZF) · [Easy Windows boxes](https://www.youtube.com/playlist?list=PLidcsTyj9JXL4Jv6u9qi8TcUgsNoKKHNn)

---

## External practice & learning

### Vulnerable machines / apps

| Resource | What | Status |
|---|---|---|
| [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) | Modern vulnerable web app (Node/Angular), full OWASP Top 10 + more | ✅ active (flagship OWASP) |
| [Metasploitable 2](https://docs.rapid7.com/metasploit/metasploitable-2-exploitability-guide/) | Vulnerable Ubuntu VM — enum + auto/manual exploitation | ✅ current |
| [Metasploitable 3](https://github.com/rapid7/metasploitable3) | Template to build a vulnerable Windows VM | 🟡 usable, but repo commit-dormant since early 2025 |
| [DVWA](https://github.com/digininja/DVWA) | Vulnerable PHP/MySQL app, tunable difficulty | ✅ actively maintained |
| [OWASP Top Ten](https://owasp.org/www-project-top-ten/) | The canonical web-risk list (2025 edition) — see also local `[[OWASP Top 10]]` | ✅ active |

*Also worth doing*: stand these up yourself in the lab — the setup (VMs, web server, configs) is its own rep.

### Tutorial sites (war-games)

| Site | Trains | Status |
|---|---|---|
| [Over The Wire](https://overthewire.org/wargames/) | Linux CLI + `Bash`, level-by-level (start: Bandit) | ✅ up |
| [Under The Wire](https://underthewire.tech/wargames) | Windows `PowerShell`, same war-games format | ✅ up |

### Blogs

- [0xdf hacks stuff](https://0xdf.gitlab.io/) — ✅ **active (~weekly)**. Fantastic retired-HTB-box walkthroughs, each with a "Beyond Root" deep-dive; also technique/CTF write-ups.
- General: for any retired box, Google the name — the same few quality blogs recur. Read several for different perspectives.

### YouTube

| Channel | Focus | Status |
|---|---|---|
| [IppSec](https://www.youtube.com/@ippsec) | In-depth walkthrough of *every* retired HTB box | ✅ active |
| [LiveOverflow](https://www.youtube.com/@LiveOverflow) | Broad technical infosec | ✅ active |
| [STÖK](https://www.youtube.com/@STOKfredrik) | Bug bounty / web app | 🟡 sporadic uploads now |
| [VbScrub](https://www.youtube.com/@vbscrub) | Active Directory exploitation | ⛔ dormant (~4 yrs, no new uploads) |

---

## Glossary
