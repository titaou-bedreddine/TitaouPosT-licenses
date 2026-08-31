# TitaouPosT-licenses — Activation Registry

License registry for TitaouPOS. The desktop app's **Activate This PC Online**
button fetches `licenses/<HWID>.json` from this repo's `main` branch.

## How to activate a new customer
1. Customer opens: **Settings → Activation** and clicks **Copy HWID**.
2. Create a file in `licenses/` named exactly `<HWID>.json`:

```json
{
  "licensed": true,
  "license_key": "TIT-XXXX-XXXX-XXXX",
  "customer_name": "Superette Example",
  "activated_at": "2026-08-31",
  "notes": "1 PC license"
}
```
3. Commit & push to `main`. The customer clicks **Activate This PC Online**
   (or restarts) — activation is instant.

## Deactivate / refund
Delete the customer's JSON file (or set `"licensed": false`) and push.

## Rules
- One file = one licensed PC (HWID is bound to the machine's volume serial).
- Pricing: 18000 DZD first PC, +5000 DZD per additional network PC.
- Keep this repo **public** (the app reads it anonymously via raw.githubusercontent).
