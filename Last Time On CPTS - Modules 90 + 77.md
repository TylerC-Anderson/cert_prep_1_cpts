> [!abstract] Last Time On… — Modules **90** (Penetration Testing Process) + **77** (Getting Started §1–11)
> A memory-jog before you pick the path back up. Skim the callouts, click any [[wikilink]] to pull the full note when you want more. Everything here is drawn from your own HTB-derived notes.
>
> **You are here:** finished the whole process model (Mod 90) and the foundations run of Getting Started through **§11 Privilege Escalation**. Next tile is **§12 Transferring Files**, then the **Nibbles** walkthrough — that's the ***~={orange}Finish the Foundations=~*** milestone (**+100 XP**, Week 34) on the [[2_Studies/Courses/Current/CERTPREP - CPTS/CPTS RPG Progression Tree|Progression Tree]].

---

## The through-line

The two modules stack: **90** gave you the *map* (how an engagement is shaped and looped), **77** gave you the *first tools* to walk it. Same phases, two altitudes.

---

## Module 90 — Penetration Testing Process

> [!info] The one idea to hold
> The process is a **loop, not a ladder.** Two stages always come first, then you branch — and every branch can drop you *back* into information gathering. Full stage map lives in [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/Pentesting Process Flow|Pentesting Process Flow]].

**The always-first pair** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/Pentesting Process Flow|Pentesting Process Flow]]):

- **Information Gathering** — you often start with nothing but a domain or an in-scope IP range, so you *build an overview of the target before touching it*.
- **Vulnerability Assessment** — *turn that information into candidate weaknesses*, via scanners and manual analysis.

**From there, four branches** — Exploitation, Post-Exploitation, Lateral Movement, or *back to Information Gathering* when you don't have enough yet. Later stages open **Proof-of-Concept** and finally **Post-Engagement**. The key recurring move: after any foothold you loop to local info gathering (a.k.a. ***~={orange}Pillaging=~***) → re-assess → act again.

**The five-stage lifecycle**: Don't fear, use the **REEPP**er (details, [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/Ethical Hacker Methodology|Ethical Hacker Methodology]]):

| *#* | *Stage*                  | *Gist*                                                         |
| --- | ------------------------ | -------------------------------------------------------------- |
| 1   | **Reconnaissance**       | Passive (OSINT, observation) → Active (scanning + enumeration) |
| 2   | **Enumeration**          | Pry deeper on what scanning found — is it *vulnerable*?        |
| 3   | **Exploitation**         | Gain access, then look around and loop back                    |
| 4   | **Privilege Escalation** | Climb rights / establish persistence                           |
| 5   | **Post-Exploitation**    | Clean up — logs, test accounts, un-obfuscated tooling          |

**Pre-engagement is a gate, not a formality** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/6_Reporting/Rules of Engagement|Rules of Engagement]]):

- **ALWAYS** find the scope, note what's *in*, avoid what's *out*.
- **ALWAYS** find the testing/disclosure guidelines and check them for changes.

**Prioritising which attack to fire** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/3_Exploitation/Exploitation in General|Exploitation in General]]): weigh three factors — **probability of success**, **complexity**, **probability of damage**. *Avoid DoS and service-breaking exploits* UNLESS the client explicitly asks. [[Exploitation in General]] carries a worked point-scoring table (RFI beats Buffer Overflow in the example).

**Keep the receipts organised** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/Suggested Organization for PenTests|Suggested Organization for PenTests]]): one folder tree per engagement — `scope`, `scans`, `logs`, `tools`, and `evidence/{credentials,data,screenshots}.`

**Where it all lands** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/6_Reporting/Reporting|Reporting]]): screenshots as proof, redact sensitive data, write vulns + severity + impact + mitigations in language both technical and non-technical readers can act on.

> [!tip] Your own playbook
> [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/Attack Methodology & Strategy|Attack Methodology & Strategy]] is where you've turned this abstract loop into concrete opening moves and a post-compromise "search for quick wins" routine. Worth a re-read once §77 tooling is fresh.

---

## Module 77 — Getting Started (§1–11)

The foundations run. Each row jogs the memory; click through for the full note.

### §1–6 — Setup & the toolkit

| *§*   | *Section*              | *What to remember*                                                         | *Pull more*                                                                                                              |
| --- | -------------------- | ------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| 1   | Infosec Overview     | The attack-lifecycle mental model that frames everything after           | [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/Ethical Hacker Methodology\|Ethical Hacker Methodology]]      |
| 2   | Pentest Distro       | Your working environment — `tmux` panes/windows + Vim, cheatsheets saved | [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/General IT Tools\|General IT Tools]]                          |
| 3   | Staying Organized    | One engagement = one folder tree (see Mod 90 above)                      | [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/Suggested Organization for PenTests\|Suggested Organization]] |
| 4   | Connecting Using VPN | `sudo openvpn user.ovpn` → wait for `Initialization Sequence Completed`  | [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/VPNs\|VPNs]]                                                  |
| 5   | Common Terms         | Ports/protocols + inline glossaries in the phase notes                   | [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/Networking Review\|Networking Review]]                        |
| 6   | Basic Tools          | `netcat` for banner-grabbing + shells; `socat` as the sturdier cousin    | [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/About Netcat\|About Netcat]]                                  |

**VPN, the parts that bite** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/VPNs|VPNs]]):

- Confirm the tunnel came up — look for a **`tun0`** adapter (`ifconfig`); `netstat -rn` shows what's reachable through it (`10.129.0.0/16` HTB machines via `tun0`).
- ***~={orange}Treat the lab VPN as hostile=~*** — VM only, no sensitive data on the attack box, never reuse a client-assessment VM for HTB.

**`netcat` = your Swiss Army knife** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/About Netcat|About Netcat]]): connect to any listening port and read its banner (**Banner Grabbing**) — e.g. hitting TCP 22 spits back the `SSH` version. `socat` adds port-forwarding and a sturdier reverse-shell upgrade path.

### §7–11 — First contact with a target

**§7 Service Scanning** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/2_Enumeration/nmap - Active Scanning|nmap - Active Scanning]])

- The 3-way handshake mnemonic — `SYN` / `SYNACK` / `ACK` → ***~={orange}"Sin-snack-ack!"=~***. Open port answers `SYNACK`; closed port answers `RST`.
- ***The CTF Special*** — `nmap -T4 -p- -A IPADDR`: fast, all ports, OS + version + default NSE + traceroute. Loud and proud — fine for CTFs/compliance work, **not** stealth.
- `-sS` "stealth" isn't stealthy anymore (SOCs watch for the RST pattern); `-sU` for UDP is slow because UDP is connectionless.

**§8 Web Enumeration** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/2_Enumeration/Enumerating HTTP and HTTPS|Enumerating HTTP and HTTPS]])

- Always eyeball: **source (Ctrl-U)**, **Dev Tools → Network** (api/token/key/internal/localhost), **robots.txt**, linked JS.
- Directory-bust with `ffuf` / `gobuster` (`FUZZ` = injection point); a **default web page** is a hygiene tell — what else did they leave lying around?

**§9 Public Exploits** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/2_Enumeration/Enumerating Vulnerabilities|Enumerating Vulnerabilities]])

- Rank targets by ease / stealth / blast-radius / post-ex value, shortlist, *then* hunt exploits.
- Juiciest ports are usually **80/443** and **139/445**. Sources: `searchsploit` (offline), Exploit-DB, CVEdetails, Vulners, Packet Storm, NIST.
- ***~={orange}Validate every finding=~*** before it touches a report — screenshots and receipts, always.

**§10 Types of Shells** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/3_Exploitation/Gaining Shell Access|Gaining Shell Access]])

- **Reverse shell** = *victim connects to you* (**Hacker `<---` Target**) — ~95% of the time.
- **Bind shell** = *you connect to the victim* (**Hacker `--->` Target**) — more common on external assessments.
- Over the lab VPN you catch callbacks on **`tun0`**; directly attached, it's `eth0`. A raw `nc` shell is dumb — remember you can [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/3_Exploitation/Upgrade shell to a TTY|upgrade it to a TTY]].

**§11 Privilege Escalation** ([[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/4_Privilege_Escalation/0_General - PrivEsc|0_General - PrivEsc]])

- Initial access is usually a low-priv user → find a *local* vuln to reach `root`/`SYSTEM`.
- First reflexes: `sudo -l`, writable cron paths (`/etc/crontab`, `/etc/cron.d`, `/var/spool/cron/…`), creds in config/log/history files.
- **SSH keys** — *read* access to `.ssh/id_rsa` → copy it, `chmod 600`, `ssh -i`. *Write* access to `.ssh/` → drop your pubkey into `authorized_keys` (only works once you already control that user).
- Automate the sweep with [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/4_Privilege_Escalation/LinPEAS, WinPEAS, & SharPEAS|PEAS scripts]] — but they're **noisy** and may miss freshly-disclosed CVEs, so keep a manual check in reserve.

---

## Resume rep — a 4-move warm-up (doing, not quizzing)

> [!example] Reconnect and re-ground before §12
> Run these live, not from memory — the point is to reload the muscle, not test recall.
> 1. Bring the tunnel up: `sudo openvpn user.ovpn` → wait for `Initialization Sequence Completed`.
> 2. Prove it: `ifconfig` shows **`tun0`**; `netstat -rn` shows the HTB net behind it.
> 3. Map a box with the **CTF Special**: `nmap -T4 -p- -A <target>`.
> 4. Say out loud which way a **reverse** vs **bind** shell points, then set a `nc -lvp 4444` listener.
>
> Want a fuller, checklisted lab for §7–§11? Run **`/generate-lab`** — it'll build an active rep instead of a recall quiz.

---

> [!success] Next tile
> **§12 Transferring Files** → then the **Nibbles** walkthrough (§13–18). Clearing them banks the **+100 XP** *Finish the Foundations* milestone and unlocks the Enumeration arc.
