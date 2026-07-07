# Deploying palespruce.com

## Status
- Repo pushed to `github.com/amick/palespruce-com`, `main` branch.
- GitHub Pages not yet cut over -- DNS still points at the old GoDaddy-hosted WordPress site.
- DNS is managed through GoDaddy (same account as hosting).

## Steps to cut over (do this when ready -- the current live site goes down as soon as DNS propagates)

1. In the `palespruce-com` GitHub repo: **Settings -> Pages** -> set source to deploy from `main` / root (if not already done).
2. In that same Pages settings screen, add `www.palespruce.com` as the custom domain. This creates/updates the `CNAME` file in the repo.
3. Log into GoDaddy -> **My Products -> DNS** (or Domain Manager) for palespruce.com.
4. Find the `www` CNAME record. Change its value from `palespruce.com` to `amick.github.io`.
5. (Optional, only if you also want the bare `palespruce.com` with no `www` to work) Replace the `@` (root) A record(s) with GitHub's four Pages IPs:
   - 185.199.108.153
   - 185.199.109.153
   - 185.199.110.153
   - 185.199.111.153
6. Save changes in GoDaddy. DNS propagation is usually fast (minutes to a couple hours), but can take up to 24-48 hours in rare cases.
7. Back in GitHub repo Settings -> Pages, the domain check should go from "improperly configured" to verified once DNS propagates. No action needed on GitHub's side other than waiting/refreshing.
8. Once verified, check the **Enforce HTTPS** checkbox in Pages settings (may take a few minutes to become available after verification -- GitHub is issuing a Let's Encrypt cert at that point).

## Rollback
If anything goes wrong, GoDaddy DNS changes can be reverted by changing the `www` CNAME back to `palespruce.com` (and restoring the original `A` record on `@` if that was also changed). The old WordPress hosting itself is untouched by any of this -- only DNS routing changes.
