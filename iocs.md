# Indicators of Compromise (IOCs) — Sample 1

All values are defanged. Do not visit or resolve them from a production network.

## Network indicators

| Type | Value | Status (checked 2026-10-21) |
|---|---|---|
| Domain | `blog1seguimentmydomaine2bra[.]me` | Not registered (NXDOMAIN) |
| URL | `hxxps://blog1seguimentmydomaine2bra[.]me/` | Dead |
| IPv4 | `137[.]184[.]34[.]4` | DigitalOcean (AS14061); likely reassigned |
| Sender hostname | `ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06` | Appeared in Received, Message-Id and Return-Path headers |

## Email indicators

| Type | Value |
|---|---|
| Sender address (spoofed brand) | `banco.bradesco@atendimento[.]com[.]br` |
| Return-Path | `root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06` |
| Subject | `CLIENTE PRIME - BRADESCO LIVELO: Seu cartão tem 92.990 pontos LIVELO expirando hoje!` |
| Message-Id | `<20230919183549.39DEA3F725@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06>` |

## File indicators

| Type | Value |
|---|---|
| SHA-256 (`sample-1.eml`) | `35ef116a75e5e46e6859b49b60a23b4ddfe5f91d1368e0fc67a16df698cb96e0` |

## MITRE ATT&CK mapping

| Tactic | Technique | Evidence |
|---|---|---|
| Initial Access | T1566.002 Phishing: Spearphishing Link | Email carries a link to an external lure page |
| Defense Evasion | T1656 Impersonation | Pretends to be Bradesco / Livelo |
| Resource Development | T1583.001 Acquire Infrastructure: Domains | Throwaway lure domain |
| Resource Development | T1583.003 Acquire Infrastructure: Virtual Private Server | Email sent from a rented cloud server |

Note: the last two are inferred from the infrastructure, not from observed attacker activity.
