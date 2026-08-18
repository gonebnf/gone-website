# gonelegacy.com

Static homepage for Gone (Beyond the Gates Inc.), served by GitHub Pages.

## Layout

```
index.html          single-page site, CSS inlined, no build step
404.html            not-found page
CNAME               custom domain (gonelegacy.com)
assets/favicon.svg  site icon
assets/inter-var.woff2  self-hosted variable font
robots.txt, sitemap.xml
```

## Editing

Edit `index.html` and push to `main` — Pages redeploys automatically.
There is no build step and no dependencies.

Preview locally:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Contact form

The "Get in touch" buttons are `mailto:hello@gonelegacy.com`. There is no backend.

Note on where that mail goes: `gonelegacy.com` uses **Cloudflare** nameservers
(`igor.ns.cloudflare.com`, `zara.ns.cloudflare.com`), and its MX records point to
Cloudflare Email Routing — not to AWS SES. The SES receipt rule and
`ses-email-forwarder` Lambda still exist in AWS but receive nothing, because no MX
record directs mail to `inbound-smtp.us-east-1.amazonaws.com`. Confirm
`hello@gonelegacy.com` is configured as a route in Cloudflare Email Routing.

SES outbound sending does work: the three `_domainkey` DKIM CNAMEs are published in
Cloudflare, so DKIM passes. The SPF record is `v=spf1 include:_spf.mx.cloudflare.net ~all`
and does **not** include `amazonses.com`, so SES-sent mail relies on DKIM alone.

## DNS

Cloudflare is authoritative. The Route 53 hosted zone in AWS still exists but nothing
queries it — the registrar delegates to Cloudflare.

    gonelegacy.com      CNAME -> gonebnf.github.io   (proxied)
    www.gonelegacy.com  CNAME -> gonebnf.github.io   (proxied)

Because Cloudflare proxies the traffic, TLS is terminated by Cloudflare (Let's Encrypt),
and GitHub's own "Enforce HTTPS" stays unavailable (`cert_state=none`). Keep the
Cloudflare SSL/TLS mode on **Full** so the Cloudflare-to-GitHub leg is encrypted.

## History

Replaces an Astro app that ran on EC2 behind CloudFront. That infrastructure was
decommissioned 2026-08-18 to remove ~$158/month of AWS spend; SES, Route 53, and the mail
forwarder were deliberately kept. Copy here is adapted from the previous homepage, with
unverified claims (customer counts, security certifications, testimonials) removed.
