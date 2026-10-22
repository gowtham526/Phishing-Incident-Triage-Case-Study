# Header Analysis — Sample 1 (Fake Bradesco / Livelo)

**File:** `samples/sample-1.eml`
**SHA-256:** `35ef116a75e5e46e6859b49b60a23b4ddfe5f91d1368e0fc67a16df698cb96e0`

## Key headers

| Header | Value |
|---|---|
| Subject | CLIENTE PRIME - BRADESCO LIVELO: Seu cartão tem 92.990 pontos LIVELO expirando hoje! |
| From (display) | BANCO DO BRADESCO LIVELO <banco.bradesco@atendimento[.]com[.]br> |
| Return-Path | root@ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06 |
| Sender IP | 137[.]184[.]34[.]4 |
| Date | Tue, 19 Sep 2023 18:35:49 +0000 |
| SPF | temperror (DNS timeout; not a pass) |
| DKIM | none (message not signed) |
| DMARC | temperror, action=none |
| compauth | fail (reason 001) |
| Microsoft SCL | 5 (spam) |

## Delivery path (oldest to newest)

1. Created by Postfix on `ubuntu-s-1vcpu-1gb-35gb-intel-sfo3-06`, run by `root` (userid 0), 18:35:49 UTC.
2. Handed to Microsoft EOP from 137[.]184[.]34[.]4 at 18:36:44 UTC.
3. Internal Microsoft hops to the recipient mailbox, 18:36:45–46 UTC (normal).

## Findings

1. **Sender mismatch.** The visible sender claims to be Bradesco, but the real return path is `root@` on an unnamed cloud server. A bank does not send mail like this.
2. **No authentication passed.** DKIM was absent and the Microsoft composite check failed (`compauth=fail`).
3. **Origin is a throwaway server.** The first hop is a bare Postfix install run as root.
4. **Consistent timestamps.** The Date header matches the first hop, so the time was not forged.

## Caveat

SPF and DMARC returned `temperror` because a DNS lookup timed out. That alone does not prove spoofing. The conclusion rests on the Return-Path mismatch, the missing DKIM signature, and the failed `compauth`.

## Verdict

Phishing: impersonates Bradesco/Livelo to lure the recipient to a credential-harvesting page.
