# Analysis — Sample 2 (Fake Mashreq Bank "Verify Your Email")

**File:** `samples/sample-2.eml`
**SHA-256:** `cd7cf5bd51735184850f8ff10966ec15a93f53f4d976f9860a359528359e62aa`

## Key headers

| Header | Value |
|---|---|
| Subject | Confirm Your Mashreq Email Now For Your Security (MOVE TO INBOX) |
| From | MashreqAlerts <postmaster@digitalmashreq[.]mg[.]tdi[.]tc> |
| Return-Path | Mailgun bounce address at `mg[.]tdi[.]tc` |
| Sender IP | 143[.]55[.]232[.]5 (`pc232-5.mailgun[.]net`) |
| Date | Wed, 20 Sep 2023 10:49:41 +0000 |
| SPF | none |
| DKIM | fail (no key for signature) |
| DMARC | fail |
| compauth | fail (reason 001) |

## Delivery path

1. Submitted over HTTP to the Mailgun bulk-mail service (`Received: from <unknown> ... with HTTP`).
2. Sent from Mailgun host `pc232-5.mailgun[.]net` (143[.]55[.]232[.]5).
3. Delivered via Microsoft EOP to the recipient mailbox.

## Link analysis (no link was opened)

| Item | Detail |
|---|---|
| Visible button | "Sign in To verify your email" |
| Actual link | A `bing[.]com/ck/a?...` redirect wrapper |
| Decoded final destination | `hxxp://marhaba-travel[.]com/fr/formules` |
| Relation to Mashreq | None. A travel website. |

The scammer hides the real destination behind a trusted search-engine redirect, so link filters and users see "bing.com". The destination is a travel site, probably compromised or abused. Its live content was not examined.

## Red flags

1. Sender domain `tdi[.]tc` is unrelated to Mashreq Bank.
2. SPF none, DKIM fail, DMARC fail, compauth fail: nothing authenticates.
3. Button hidden behind a bing.com redirect to an unrelated travel site.
4. Subject says "(MOVE TO INBOX)": asks the reader to rescue it from spam.
5. Pressure: "our previous email was ignored. Please address the instructions promptly."
6. Brand images are loaded from the real mashreqbank.com site to look authentic.
7. Generic greeting ("Dear Client").

## Verdict

**Credential-harvesting phishing** impersonating Mashreq Bank. The goal is to move the user to a fake "verify your email" login page.

## Recommended response

1. Do not click the button. Report as phishing and delete.
2. Block the sender domain `mg[.]tdi[.]tc` / `tdi[.]tc` on the mail gateway.
3. Block `marhaba-travel[.]com` at the web proxy as a precaution, and notify the site owner (likely compromised).
4. **Do not block** 143[.]55[.]232[.]5. It is shared Mailgun infrastructure.
5. If a user already clicked or entered credentials: reset their password, revoke sessions, and watch the account.

## IOCs

| Type | Value |
|---|---|
| Sender address | `postmaster@digitalmashreq[.]mg[.]tdi[.]tc` |
| Sender domain | `digitalmashreq[.]mg[.]tdi[.]tc` / `tdi[.]tc` |
| Final link domain | `marhaba-travel[.]com` |
| Final URL | `hxxp://marhaba-travel[.]com/fr/formules` |
| Redirect wrapper | `hxxps://www[.]bing[.]com/ck/a?...` (abused, legitimate service) |
| Sender IP | `143[.]55[.]232[.]5` (Mailgun, shared; do not block) |
| Subject | `Confirm Your Mashreq Email Now For Your Security (MOVE TO INBOX)` |

## MITRE ATT&CK

| Technique | Evidence |
|---|---|
| T1566.002 Phishing: Spearphishing Link | Button leads to an external page |
| T1656 Impersonation | Pretends to be Mashreq Bank |

Note: abuse of a legitimate bulk-mail service (Mailgun) and of a search-engine redirect is an observed tactic here, but it is not mapped to a specific technique ID.
