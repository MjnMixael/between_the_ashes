# Between the Ashes — website

Static one-page site for the *Between the Ashes* FreeSpace 2 mod, hosted on GitHub Pages.

## Layout
- `website/` — the published site:
  - `index.html` — the entire site (self-contained: inline CSS + inline jQuery, no build step, no server code)
  - `images/` — screenshots, logo, favicon
  - `CNAME` — GitHub Pages custom-domain config
- `.github/workflows/deploy.yml` — publishes `website/` to GitHub Pages on every push to `master`

There is no backend. Download links point out to fsnebula.org and the Knossos release page; the
site itself serves nothing but the page and its images.

## Domains

| Domain | Role | How |
| --- | --- | --- |
| `betweentheashes.com` | **Canonical** — serves the site, gets the HTTPS cert | In `website/CNAME`; DNS points at GitHub Pages |
| `btagame.com` | Redirect → `https://betweentheashes.com` | Registrar URL forwarding (301, with SSL) |

GitHub Pages only supports one custom domain per repo (the one in `CNAME`), so the second domain
redirects to the first at the registrar rather than via GitHub.

## DNS — `betweentheashes.com` (canonical)

Apex `A` records:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```
Apex `AAAA` records:
```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```
`www` subdomain — `CNAME` → `MjnMixael.github.io`

## DNS — `btagame.com` (redirect)

Use the registrar's URL forwarding (Porkbun: "URL Forwarding"), 301 + SSL:
```
btagame.com      ->  https://betweentheashes.com
www.btagame.com  ->  https://betweentheashes.com
```

## Deploy
Push to `master`; the workflow builds and publishes automatically. Then in **Settings → Pages**:
custom domain = `betweentheashes.com`, enable **Enforce HTTPS** once the certificate provisions.
