# TitaouPosT-licenses — Activation & Revocation Registry

License registry for **TitaouPOS** (v0.6.0 signed-licensing era). The POS
reads this repo anonymously via raw.githubusercontent — keep it **public**.

## Files
- `licenses/<HWID>.json` — per-machine signed license (published by the
  developer's **License Generator** tool). The client's *Activate This PC
  Online* button pulls it and activates through signature verification.
- `revoked.json` — `{"revoked": ["HW-…"]}`. A listed machine flips to
  READ-ONLY in every TitaouPOS within ~30 minutes (or at its next
  activation attempt). The serial can never be reused on another PC.

## How a client activates (v0.6.0)
1. Setup wizard (step 4) or Settings → Activation shows a **request code**
   (HWID + shop + owner) with a copy button and a QR.
2. The developer pastes it into the standalone **License Generator**,
   chooses Full (lifetime) or Trial (N days) and signs.
3. Delivery — any of:
   - **.lic file** (preferred): the client drags & drops it in Settings →
     Activation.
   - **Serial key**: paste + Activate.
   - **Publish Online** (generator button): writes `licenses/<HWID>.json`
     here; the client clicks *Activate This PC Online* — no typing.
   - **Telegram**: the POS's approval card (Full / Trial 14d / Reject).
4. The POS verifies the **Ed25519 minisign signature** against the public
   key embedded in the app build, checks the HWID matches this machine and
   the trial expiry — only then activation persists.

## Revocation (refunds / unpaid machines)
In the License Generator: paste the HWID → **Revoke** (adds it to
`revoked.json`). **Un-revoke** removes it when a new license is issued.

## Rules
- One license = one PC (HWID = volume serial + hostname hash).
- The JSON here is only TRANSPORT — the signature is the trust boundary;
  a client with the bot token or DB access cannot forge a license.
- Pricing: 18000 DZD first PC, +5000 DZD per additional network PC.
