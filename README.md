# SHX TOKEN — Cloudflare Pages

A responsive, static website for the supplied Stellar asset identifier. It uses no build step or external JavaScript libraries.

## Files

- `index.html` — complete responsive site, animations and live market panel.
- `assets/shx-mark.png` — the supplied SHX TOKEN logo used by the site and metadata.
- `assets/shx-mark.svg` — supplementary vector token artwork.
- `Stellar.toml` — easy-to-find copy of the asset metadata.
- `.well-known/stellar.toml` — standard public location for Stellar TOML metadata.
- `_headers` — basic browser security headers, including access to Stellar Horizon for the live quote.
- `wrangler.toml` — Cloudflare Pages project configuration.

## Deploy to `https://shxxlm.pages.dev/`

1. In Cloudflare, open **Workers & Pages → Create → Pages → Direct Upload** (or create a Pages project named `shxxlm`).
2. Upload the contents of this folder, keeping the `.well-known` directory and `assets` directory intact.
3. Cloudflare will serve the site at the project's `*.pages.dev` address. The project name must be `shxxlm` for the requested address `https://shxxlm.pages.dev/` to be used.

Alternatively, after authenticating Wrangler with your Cloudflare account, run from this folder:

```bash
npx wrangler pages deploy . --project-name shxxlm
```

The deployment target must be a Pages project you own or are authorized to update. These files are deployment-ready, but this package does not publish to your Cloudflare account automatically.

## Live market panel

The page queries the public Stellar Horizon endpoint for the exact `SHX` / issuer pair and the XLM order book. It shows an indicative midpoint when both sides exist, a one-sided quote when only a bid or ask exists, and `NO LIVE QUOTE` when there are no visible offers. It never substitutes the price of a different SHX issuer. Quotes refresh every 30 seconds.

## Issuer identity warning

The supplied issuer is:

`GBSQFHA3PDQPKG4QKJ2GMQIZASFVLQDO3YF3K7IG2CULIHMTMKZCLSTX`

This differs from the issuer published for Stronghold's SHx token, which begins `GDSTRSHX`. Stellar asset codes are not unique; the issuer address is part of the asset identity. This site follows only the issuer address supplied in the request and does not claim affiliation with Stronghold.

## Stellar TOML

After deployment, the standard metadata URL will be:

`https://shxxlm.pages.dev/.well-known/stellar.toml`

The token image URL is:

`https://shxxlm.pages.dev/assets/shx-mark.png`

For Stellar TOML domain verification, the domain must serve the file successfully and the asset's home domain must be set to the same domain by the issuer account. Publishing this file alone does not modify the Stellar issuer account's home-domain setting.
