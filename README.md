# Phishing Incident Triage — Case Study

Triage of three real phishing / scam emails, written the way a SOC analyst would hand it over: headers, links, verdict, IOCs, response steps and detection rules.

**Sources:** real samples from the public [Phishing Pot](https://github.com/rf-peixoto/phishing_pot) honeypot collection (emails from September 2023, analysed October 2026).
**Environment:** Kali Linux VM. Samples read as text only; no link was opened and no attachment was executed.

## Results at a glance

| # | Sample | Type | Impersonates | Auth result | Key evidence |
|---|---|---|---|---|---|
| 1 | `sample-1.eml` | Credential / card phishing | Bradesco / Livelo (Brazil) | SPF temperror, DKIM none, DMARC temperror, compauth **fail** | Return-Path is `root@` on a throwaway cloud server; link to an unrelated `.me` domain |
| 2 | `sample-2.eml` | Credential phishing | Mashreq Bank | SPF none, DKIM fail, DMARC fail, compauth **fail** | Sign-in button hidden behind a bing.com redirect to an unrelated travel site; sent through abused Mailgun |
| 3 | `sample-3.eml` | Advance-fee / inheritance scam | A made-up person | SPF, DKIM, DMARC **all pass** | Passes authentication but uses hidden mass recipients and a classic "inheritance" story |

## Method

1. **Headers:** compare From / Return-Path / Reply-To, read the Received chain bottom-up, read SPF / DKIM / DMARC.
2. **Content:** urgency, fear or reward, generic greeting, requests for credentials or bank details.
3. **Links and attachments:** extract and defang links, decode redirects without visiting them, check domain and IP in VirusTotal, AbuseIPDB, WHOIS and DNS.
4. **Verdict, IOCs and MITRE mapping**, then recommended response.
5. **Detection:** Sigma rules and Splunk searches built from the patterns found.

## Repository layout

## What this case study shows

- **Passing SPF/DKIM/DMARC does not mean an email is safe.** Sample 3 passes everything and is still a scam. Authentication proves where mail came from, not whether it is honest.
- **Reputation data expires.** The phishing domain in sample 1 is no longer registered (NXDOMAIN, "Domain not found") and the sender IP now belongs to a different tenant. Clean scores today do not describe 2023, so the verdict rests on the email's own evidence.
- **Shared infrastructure must not be blocked blindly.** Mailgun and Gmail addresses in samples 2 and 3 are shared. The correct control is blocking the sender domain or account, not the IP.
- **Trusted domains can hide the real destination.** Sample 2 wraps its link in a bing.com redirect.

## Limitations

- Landing pages were already offline, so the credential-harvesting purpose of samples 1 and 2 is inferred from the email content, not from a captured page.
- Detection rules use generic field names and have not been run against live email logs.
- MITRE mappings for infrastructure are inferred, not observed attacker activity.

## Tools

Kali Linux, `curl`, `sha256sum`, `grep`, `dig`, `whois`, Python 3, VirusTotal, AbuseIPDB, urlscan.io, Sigma, Splunk SPL.

## License

MIT. See `LICENSE`.
