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

The "Get in touch" buttons are `mailto:hello@gonelegacy.com`. That address is received by
AWS SES (receipt rule `forward-all-emails` on the `gonelegacy.com` domain) and forwarded by
the `ses-email-forwarder` Lambda to gonebnf2025@gmail.com. There is no backend.

## History

Replaces an Astro app that ran on EC2 behind CloudFront. That infrastructure was
decommissioned 2026-08-18 to remove ~$158/month of AWS spend; SES, Route 53, and the mail
forwarder were deliberately kept. Copy here is adapted from the previous homepage, with
unverified claims (customer counts, security certifications, testimonials) removed.
