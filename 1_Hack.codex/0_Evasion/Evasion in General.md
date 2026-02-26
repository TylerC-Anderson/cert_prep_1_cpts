
## Quick-Use

**Commands**:

*Tools*:
- 

## General

**Objectives**:

**Overview**:

If a skilled administrator monitors the systems, any change or even a single command could trigger an alarm that will give us away. In many cases, we get kicked out of the network, and then threat hunting begins where we are the focus. We may also lose access to a host (that gets quarantined) or a user account (that gets temporarily disabled or the password changed). This penetration test would have failed but succeeded in some ways because the client could detect some actions. We can provide value to the client in this situation by still writing up an entire attack chain and helping them identify gaps in their monitoring and processes where they did not notice our actions. For us, we can study how and why the client detected us and work on improving our evasion skills. Perhaps we did not thoroughly test a payload, or we got careless and ran a command such as `net user` or `whoami` that is often monitored by EDR systems and flagged as anomalous activity.

It can often help our clients if we run commands or tools that their defenses stop or detect. It shows them that their defenses are working on some attacks. Keep in mind that we are emulating an attacker, so it's not always entirely bad for some of the attacks to get noticed. Though when performing evasive testing, our goal should be to go mostly undetected so we can identify any "blind spots" our clients have in their network environments.

Evasive testing is divided into three different categories:

| **`Evasive`** | **`Hybrid Evasive`** | **`Non-Evasive`** |
| ------------- | -------------------- | ----------------- |

This does not mean that we cannot use all three methods. Suppose our client wants to perform an intrusive penetration test to get as much information as possible and the most in-depth testing results. In that case, we will perform `Non-Evasive` Testing, as the security measures around the network may limit and even stop us. However, this can also be combined with `Evasive` testing, using the same commands and methods for non-evasive testing. We can then see if the security measures can identify and respond to the actions performed. In `Hybrid-Evasive` testing, we can test specific components and security measures that have been defined in advance. This is common when the customer only wants to test specific departments or servers to see if they can withstand the attacks.

## Glossary