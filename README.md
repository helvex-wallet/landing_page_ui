# Helvex Landing Page

Static, self-contained landing page for Helvex — RFQ swaps on Canton Network.

The entire site lives in a single file: [`index.html`](./index.html) (all CSS/JS inline; only external dependency is Google Fonts over HTTPS).

## Deployment (Vercel)

The site is deployed on [Vercel](https://vercel.com). It's a plain static site — `index.html` at the repo root is served automatically, so no build step is required. [`vercel.json`](./vercel.json) only enables clean URLs.

### First-time setup

1. In Vercel, click **Add New → Project** and import the `helvex-wallet/landing_page_ui` repo.
2. Framework preset: **Other**. Leave the build command empty and set the output directory to the repo root (default) — this is a static site, no build step.
3. Deploy. Every push to `main` will auto-deploy; pull requests get preview URLs.

## Custom domain: `helvex.cc`

1. In the Vercel project, go to **Settings → Domains** and add `helvex.cc` (and optionally `www.helvex.cc`).
2. Vercel will show the exact DNS records to add. For an apex domain it's typically one of the two options below.

### DNS records to add at your registrar

**Option A — A record (apex domain):**

| Type | Host / Name | Value          |
| ---- | ----------- | -------------- |
| A    | `@`         | `76.76.21.21`  |

**Option B — Nameservers (let Vercel manage DNS):**
Point `helvex.cc` at Vercel's nameservers (shown in the dashboard, e.g. `ns1.vercel-dns.com` / `ns2.vercel-dns.com`). This lets Vercel handle everything automatically.

**`www` subdomain redirect (optional):**

| Type  | Host / Name | Value                  |
| ----- | ----------- | ---------------------- |
| CNAME | `www`       | `cname.vercel-dns.com` |

> Always use the exact values shown in **your** Vercel Domains tab — they can differ per project/region. The values above are Vercel's common defaults.

### After DNS is configured

- Wait for propagation (usually minutes). Verify with:
  ```bash
  dig helvex.cc +short
  ```
- Vercel provisions a free TLS certificate automatically once the domain validates; the site will be live at **https://helvex.cc**.
