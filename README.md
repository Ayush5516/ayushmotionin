# Ayush Edits

A single-page portfolio and booking site for Ayush Edits, a freelance video editor and motion designer. The site showcases categorized video work (real estate, talking head, UGC ads, SaaS/animation), presents pricing packages, and lets visitors book a project via WhatsApp.

## Key technologies

- Plain HTML5 with [Tailwind CSS](https://tailwindcss.com) loaded via the CDN script, configured inline for a dark/gold theme
- [Font Awesome](https://fontawesome.com) for icons and Google Fonts (Inter) for typography
- Vanilla JavaScript for the mobile menu toggle, pricing package selection, and the booking form's WhatsApp handoff
- Deployed as a static site on Netlify (see `netlify.toml`)

## Running locally

No build step or dependencies are required. Either:

- Open `index.html` directly in a browser, or
- Serve it locally with the Netlify CLI: `netlify dev --port 8889` from the project root, then visit `http://localhost:8889`

## Structure

- `index.html` — the entire site (header/nav, hero, portfolio, pricing, booking form, footer)
- `netlify.toml` — publishes the project root as the static site
