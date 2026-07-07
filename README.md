# Helvex Landing Page

Static, self-contained landing page for Helvex — RFQ swaps on Canton Network.

The entire site lives in a single file: [`helvex-landing.html`](./helvex-landing.html) (all CSS/JS inline; only external dependency is Google Fonts over HTTPS).

## Deployment

Deployment is automated via GitHub Actions ([`.github/workflows/deploy.yml`](./.github/workflows/deploy.yml)). On every push to `main`, the workflow copies `helvex-landing.html` to `index.html`, writes the `CNAME` file, and publishes to GitHub Pages.

One-time setup: in the repo, go to **Settings → Pages → Build and deployment → Source** and select **GitHub Actions**.

You can also trigger a deploy manually from the **Actions** tab (`workflow_dispatch`).

## Custom domain: `helvex.cc`

The site is served at **https://helvex.cc**. `helvex.cc` is an apex (root) domain, so it needs `A` records (and optionally `AAAA` for IPv6) pointing at GitHub Pages.

### DNS records to add at your registrar

**A records** (required — point the apex `@` at GitHub Pages IPv4 addresses):

| Type | Host / Name | Value             |
| ---- | ----------- | ----------------- |
| A    | `@`         | `185.199.108.153` |
| A    | `@`         | `185.199.109.153` |
| A    | `@`         | `185.199.110.153` |
| A    | `@`         | `185.199.111.153` |

**AAAA records** (optional — IPv6 support):

| Type | Host / Name | Value                    |
| ---- | ----------- | ------------------------ |
| AAAA | `@`         | `2606:50c0:8000::153`    |
| AAAA | `@`         | `2606:50c0:8001::153`    |
| AAAA | `@`         | `2606:50c0:8002::153`    |
| AAAA | `@`         | `2606:50c0:8003::153`    |

**CNAME record** (optional — so `www.helvex.cc` also works and redirects to the apex):

| Type  | Host / Name | Value                       |
| ----- | ----------- | --------------------------- |
| CNAME | `www`       | `helvex-wallet.github.io.`  |

### After DNS is configured

1. Wait for DNS to propagate (usually minutes, up to 24h). Verify with:
   ```bash
   dig helvex.cc +short
   ```
   It should return the four `185.199.108–111.153` addresses.
2. In the repo, go to **Settings → Pages** and confirm the custom domain shows `helvex.cc` with a green check.
3. Enable **Enforce HTTPS** (GitHub provisions a free TLS certificate automatically once DNS validates).

> The `CNAME` file is written automatically by the deploy workflow, so it survives every redeploy — do not rely on setting the domain only in the Pages UI.
