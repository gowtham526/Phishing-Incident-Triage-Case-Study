# Analysis — Sample 3 (Inheritance / Advance-Fee Scam)

**File:** `samples/sample-3.eml`
**SHA-256:** `6fd8e6fe726a67236792221d307a7eb84b805c38293901e2971a6c8240451004`

## Key headers

| Header | Value |
|---|---|
| Subject | Dia Bom |
| From | Nora Alex <noraalex01@gmail[.]com> |
| Return-Path | noraalex12345@gmail[.]com |
| To | undisclosed-recipients:; |
| Sender IP | 209[.]85[.]208[.]43 (Google mail server) |
| Date | Tue, 19 Sep 2023 12:11:27 +0000 |
| SPF / DKIM / DMARC | **pass / pass / pass** |
| compauth | pass |

## Delivery path

1. Sent through Gmail (`mail-ed1-f43.google[.]com`, 209[.]85[.]208[.]43).
2. Delivered via Microsoft EOP to the recipient mailbox. Normal routing.

## Why this is a scam even though authentication passes

SPF, DKIM and DMARC prove the message came from Gmail's servers. They do not prove the sender is trustworthy. A scammer using a free Gmail account passes all of them.

## Red flags

1. **Hidden mass recipients.** `To: undisclosed-recipients` shows a bulk send.
2. **Two different sender accounts.** `From` is `noraalex01@gmail[.]com`, `Return-Path` is `noraalex12345@gmail[.]com`.
3. **Impersonal opening.** "Querido" (Dear) with no name, written to many people.
4. **Classic advance-fee story.** A stranger with an inheritance asks the recipient to (1) provide a new empty bank account, (2) act as "guardian" of the funds, and (3) help arrange residency in the recipient's country.
5. **Urgency to reply.** Asks the recipient to respond as soon as possible.
6. **Vague subject.** "Dia Bom" ("Good day") reveals nothing.

## Link and attachment analysis

None. No URLs and no attachments, so there is nothing to submit to VirusTotal or urlscan. The risk comes from the conversation that follows: requests for a bank account and personal details.

## Verdict

**Advance-fee / inheritance scam (social engineering).** Not a malware or credential-harvesting email. Intended outcome: build trust, then obtain bank details, money or identity documents.

## Recommended response

1. Do not reply and do not send any bank or personal details.
2. Report as phishing in the mail client and block the sender.
3. Delete the message.
4. If a user already replied or shared details, escalate: warn them, and advise contacting their bank.

## IOCs

| Type | Value |
|---|---|
| Email | `noraalex01@gmail[.]com` |
| Email (Return-Path) | `noraalex12345@gmail[.]com` |
| Sender IP | `209[.]85[.]208[.]43` (Google, shared infrastructure, **do not block**) |
| Subject | `Dia Bom` |

## MITRE ATT&CK

No exact technique fits. This is fraud by social engineering without a technical payload. The closest is **T1656 Impersonation**, because the sender uses a made-up identity and backstory. The sender IP is Google's shared mail infrastructure, so blocking it would block legitimate mail. The correct controls are user awareness and sender-level reporting.
