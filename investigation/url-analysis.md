# URL & Infrastructure Analysis — Sample 1

## Links found in the email body

| Link | Verdict | Notes |
|---|---|---|
| `hxxps://blog1seguimentmydomaine2bra[.]me/` | **Malicious (phishing lure)** | Call-to-action link. Domain has no relation to Bradesco or Livelo. |
| `hxxps://fonts[.]googleapis[.]com/...` | Benign | Web font used for page styling. |
| `hxxps://fonts[.]gstatic[.]com` | Benign | Google font hosting. |

## Lookups performed (2026-10-21, no link was opened)

| Check | Result |
|---|---|
| VirusTotal URL (`http://` form) | 0 / 93, clean today |
| DNS (`dig`) | **NXDOMAIN**, domain does not resolve |
| WHOIS (`whois`) | **"Domain not found"**, not registered |
| Sender IP 137[.]184[.]34[.]4, WHOIS | DigitalOcean, LLC (US), cloud hosting |
| Sender IP, AbuseIPDB | 13 reports, 0% abuse confidence; reverse DNS now shows a Cloudways hosting hostname |
| Sender IP, VirusTotal | 0 / 92, 1 vendor "suspicious" |

## Analysis

1. The lure domain is unrelated to the impersonated brand and uses a `.me` ending. The long, jumbled name is typical of throwaway phishing domains.
2. The domain **no longer exists**. This is consistent with a takedown or expiry after the September 2023 campaign. Clean reputation scores today therefore say nothing about the domain's state in 2023.
3. The sender IP belongs to a public cloud provider. Cloud IPs are recycled, so today's low abuse score and Cloudways hostname most likely reflect a **different tenant**, not the original sender.
4. The page itself could not be examined because the site is gone. The credential-harvesting purpose is inferred from the email content (urgent "points expiring today" lure impersonating a bank) and not from a captured landing page.

## Limitation

Indicators in this case have expired. The verdict rests on the email's own evidence (sender mismatch, failed authentication, unrelated link domain), not on current threat-intelligence hits.
