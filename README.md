# bank-recon-callback

Static OAuth redirect target for [bank-recon](../bank-recon/). One HTML file. Hosted as GitHub Pages at <https://ggrigo.github.io/bank-recon-callback/>.

When a bank redirects the user back after PSD2 SCA, the URL looks like:

```
https://ggrigo.github.io/bank-recon-callback/?code=<auth_code>&state=<uuid>
```

This page displays `code`, `state`, and the full URL, with a copy-to-clipboard button. The user pastes the URL back into the local `authorize.py` script, which exchanges the code for a long-lived Enable Banking session.

## Why a separate repo

So this can be public (GitHub Pages requires public for the free tier) while [bank-recon](../bank-recon/) stays private. Two repos keeps us on the GitHub free plan and physically separates the OAuth endpoint from anything sensitive.

## What's NOT here

- No application secrets, no `.pem`, no API keys, no analytics, no telemetry, no external scripts.
- Nothing is sent anywhere — the `code` and `state` values live only in the user's browser tab.

## Enabling GitHub Pages

After pushing to GitHub:

1. Repo **Settings** → **Pages**
2. **Source**: Deploy from a branch
3. **Branch**: `main`, folder: `/ (root)`
4. Save. Wait ~1 minute. Page is live at `https://ggrigo.github.io/bank-recon-callback/`.

## Local test

```bash
cd ~/Documents/Projects/test/bank-recon-callback
python3 -m http.server 8000
# open http://localhost:8000/?code=test-code&state=test-state-uuid
```

The page should show `test-code` and `test-state-uuid` in the respective fields.
