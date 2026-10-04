# mta-sts

Serves the MTA-STS policy for **fogrugby.com** at
<https://mta-sts.fogrugby.com/.well-known/mta-sts.txt> via GitHub Pages.

MTA-STS tells sending mail servers to require TLS when delivering to our
Google Workspace MX (`smtp.google.com`).

## Files

- `.well-known/mta-sts.txt` — the policy. Currently `mode: testing`.
- `CNAME` — the Pages custom domain, `mta-sts.fogrugby.com`.
- `.nojekyll` — required. Without it Jekyll skips dot-directories and
  `.well-known` returns 404.

## Rules when changing anything

1. **Bump the TXT record id whenever the policy file changes.** The
   `_mta-sts.fogrugby.com` TXT record (`v=STSv1; id=...;`) is managed in
   Squarespace DNS. Senders only re-fetch the policy when the id changes.
   Use a new value such as `YYYYMMDDnnnn`.
2. **Update the `mx:` line before any MX change.** If the MX record moves
   to a host not listed here, publish the new `mx:` line (and bump the id)
   first, wait at least `max_age`, then change MX. Otherwise, once in
   `enforce` mode, compliant senders will refuse to deliver.

DNS: `mta-sts` is a CNAME to `san-francisco-fog-rfc.github.io`.
No credentials are stored in this repo.
