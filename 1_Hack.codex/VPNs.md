
## Quick-Use

**Commands**:

- Connect over `openvpn` (the `.ovpn` key is downloaded from the Academy section or the HTB platform):
```shell
sudo openvpn user.ovpn
```
Success = the final line `Initialization Sequence Completed`.

- Verify the tunnel came up — look for a `tun0` adapter:
```bash
ifconfig
```

- Show the networks reachable through the VPN:
```bash
netstat -rn
```
`10.129.0.0/16` (HTB machines) is reachable via `tun0` on the `10.10.14.0/23` net.

*Tools*:
- `openvpn` - VPN client; connects using the `.ovpn` key file

## General

**Objectives**:
Connect into a private lab/corporate network and reach its hosts as if directly attached.

**Overview**:
A `VPN` routes our traffic through the VPN server instead of our ISP, so data appears to originate from the VPN's public IP, and the channel is encrypted against eavesdropping.

![[m77-GettingStarted.png|750]]

Two remote-access types:
- `Client-based VPN` - needs client software (e.g. `openvpn`); host acts as if on the company network, reaching whatever resources the server allows.
- `SSL VPN` - the browser *is* the client; usu. scoped to web apps (email, intranet), no software install.

VPNs are not to be trusted with anonymity or full privacy, since the VPN provider (`NordVPN`, `PIA`, etc.) may be logging traffic themselves. They *are* useful for bypassing network/firewall restrictions, or as a hedge against potentially hostile nets, such as public, no password wifi. Never rely on one to shield the consequences of nefarious activity.

***~={orange}Treat the HTB/lab VPN as hostile=~***: connect only from a VM, disable SSH password auth on the attack box, lock down any web servers, and keep no sensitive data on it --> never use your client-assessment VM for HTB.

### On-path DPI eating attack traffic --> VPN out

**Symptom**: an exploit / `curl` / msf module hangs right after `Request completely sent off` (no response), but the *plain* page loads fine from the same `IP:PORT`, and the exact same command solves from `Pwnbox`.

**Cause**: on-path `DPI`/`IPS` signature-matches the attack-shaped request and *silently drops* it (a hang, not a RST). Usu. a home router's threat-protection (ASUS `AiProtection`, Netgear `Armor`, `eero Secure`) or the ISP. Only bites on ~={orange}direct public targets hit in the clear=~ — traffic inside the HTB `tun0` tunnel is opaque, so normal box work never triggers it (why it can blindside you after an entire cert of tunnelled attacks).

**Fix**: route the *host* through a commercial VPN (`NordVPN`/`PIA`/etc.), then run the attack from the VM. Encryption hides the payload from the inspector, and bypasses everything downstream of the host (router + ISP).

**Triage**: benign works + Pwnbox works + your-path attack hangs = on-path content DPI on *your* egress (not the target).
- Toggle the router `IPS` off --> works = it was the router; still hangs = ISP.
- Confirm with `sudo tcpdump -i any host TARGETIPADDR` --> request leaves, no reply on the cleartext run.

## Glossary
*VPN*: Virtual Private Network — encrypted channel into a private network over public infrastructure
*tun0*: virtual tunnel adapter created on a successful VPN connection
*DPI*: Deep Packet Inspection — middlebox reading packet *contents* (not just headers) to filter/drop
*IPS*: Intrusion Prevention System — signature-matches traffic and blocks matches inline
