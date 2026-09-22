# asenso.ph — company website

Static site for **Asenso Solutions, Inc.** It exists to satisfy two Google Play requirements:

1. **Verify your organization's website** on the Play developer account.
2. A **privacy policy URL** for the Asenso Mobile store listing (later, at app submission).

No build step, no dependencies. Plain HTML and one stylesheet.

```
index.html     landing page — the company identity block is what Google reads
style.css      all styling, light + dark
logo.svg       copied from asenso_mobile/branding/splash_logo_ios.svg
robots.txt     allow all — Google must be able to crawl this to verify it
sitemap.xml
_headers       security headers (Cloudflare Pages / Netlify syntax — see note below)
```

## This repository is public, on purpose and by constraint

`apollo-com-ph` is on GitHub Free for organizations, and GitHub Pages will not serve from a
private repository on that plan. Public is therefore the only way to host here. Two consequences
that are easy to forget:

- **Never commit anything sensitive.** No credentials, no customer data, no internal API hosts.
- **The privacy policy and terms are not in this repo.** They live in `legal-drafts/`, which is
  gitignored. They are drafted against what the app actually collects and against RA 10173 and
  the BSP consumer-protection rules, but a banking privacy policy and terms are legal
  instruments. Publishing unreviewed legal text under the company's name, publicly, is the thing
  this arrangement prevents. When the company lawyer and the Data Protection Officer sign off,
  drop `legal-drafts/` from `.gitignore` and move the files to the root in one commit.

## Before the site can be pointed at asenso.ph

Everything not yet known is marked `FILL` and renders as a **yellow box on the page**, so an
unfinished site is impossible to miss.

```sh
grep -rn 'FILL' index.html          # must return nothing before verification is submitted
```

The identity block must match the Play developer account **exactly** — registered name, address,
contact details. Google cross-checks the two, and a mismatch is a failed verification.

## Hosting

GitHub Pages, `main` branch, root folder. Plain static files, no build.

## Order of operations

1. Fill every `FILL` on `index.html` with the real company details.
2. Point `asenso.ph` at GitHub Pages.
3. DNS resolves → set the custom domain to `asenso.ph` in Settings → Pages → tick **Enforce
   HTTPS** once the certificate issues.
4. Search Console → verify the `asenso.ph` domain property (the TXT record does it).
5. Play Console → *Verify your organization's website* → `https://asenso.ph`.
6. Counsel clears the legal drafts → publish `privacy.html` and `terms.html`, restore the footer
   links, add them back to `sitemap.xml`.
7. Play Console → app listing → privacy policy URL → `https://asenso.ph/privacy.html`.
