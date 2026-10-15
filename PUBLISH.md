# Publishing the PriceWatch site permanently

The site is live today on a temporary Cloudflare quick tunnel. This folder is the
permanent copy, staged and ready to publish to GitHub Pages — a fixed URL, no
cost, no server to keep running.

Nothing here has been pushed. A GitHub login is required, and that is the one
step only the owner can do.

## What is already done

- `index.html` — the offer page (payment details, real digest values, runtime-assembled contact links).
- `digest.html` — a real generated digest, published as proof of output.
- `CNAME` — not set; add one if you attach a custom domain.
- `.github/workflows/pages.yml` — deploys this folder to Pages on every push to `main`.
- Git repository initialised with a first commit.

## The one action required

```bash
gh auth login
```

Choose `GitHub.com`, `HTTPS`, and authenticate in the browser. Then publish:

```bash
cd C:/Users/hanye/business/site
gh repo create pricewatch --public --source=. --push
gh api -X POST repos/{owner}/pricewatch/pages -f build_type=workflow
```

The site then lives at `https://<your-username>.github.io/pricewatch/` and
redeploys automatically on every push. Nothing else in this folder needs to
change.

## Before publishing, decide

1. **Keep the wallet address public?** The USDT receiving address is on the page.
   That is normal for a storefront, but it will attract spam transactions. A
   dedicated receiving address is safer than your main wallet.
2. **Use an invoice, not a bare PayPal link, for real clients.** `paypal.me`
   accepts money with no order attached; a PayPal invoice ties payment to the
   order and gives you a dispute trail.
3. **Custom domain (optional).** A domain is ~$10/year. Add it under the repo's
   Pages settings and drop a `CNAME` file in this folder with the domain name.

## Reverting

Delete the repository, or set Pages to "None" in the repository settings. The
quick-tunnel site and all local files are independent of this repo.
