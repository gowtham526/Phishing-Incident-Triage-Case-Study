# Samples

The `.eml` files are **not stored in this repo**. They come from the public
[Phishing Pot](https://github.com/rf-peixoto/phishing_pot) collection. Download and verify them:

```bash
for n in 1 2 3; do
  curl -O https://raw.githubusercontent.com/rf-peixoto/phishing_pot/main/email/sample-$n.eml
done
sha256sum sample-*.eml
```

| File | SHA-256 |
|---|---|
| sample-1.eml | `35ef116a75e5e46e6859b49b60a23b4ddfe5f91d1368e0fc67a16df698cb96e0` |
| sample-2.eml | `cd7cf5bd51735184850f8ff10966ec15a93f53f4d976f9860a359528359e62aa` |
| sample-3.eml | `6fd8e6fe726a67236792221d307a7eb84b805c38293901e2971a6c8240451004` |

Handle them as text only. Do not open links or attachments.
