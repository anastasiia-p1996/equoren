# Equoren — equoren.com

Single-page marketing site for Equoren (Operations &amp; Automation). Static, no backend, no database, no build step required.

## Files

```
Equoren.dc.html    the website (all markup, styles and behaviour)
support.js         runtime the page loads (must sit next to the HTML)
favicon.svg        favicon
robots.txt         crawl rules + sitemap pointer
sitemap.xml        single-URL sitemap
README.md          this file
```

## Run locally

Any static server from the project root:

```bash
python3 -m http.server 8080
# or
npx serve .
```

Then open `http://localhost:8080/Equoren.dc.html`.

## Deploy to Cloudflare Pages

1. Push this folder to a GitHub repository.
2. Rename `Equoren.dc.html` to `index.html` (keep `support.js` in the same folder) so `https://equoren.com/` serves the page at the root.
3. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git** → pick the repo.
4. Build settings:
   - Framework preset: **None**
   - Build command: *(leave empty)*
   - Build output directory: `/`
5. **Save and Deploy**.
6. **Custom domains** → add `equoren.com` and `www.equoren.com`, follow the DNS prompt (Cloudflare adds the CNAME automatically if the domain is on Cloudflare).

No environment variables are required.

## Contact form

The form has no backend. Out of the box it opens the visitor's email client with the inquiry pre-filled and sends nothing to any server — there is no placeholder endpoint being posted to.

To switch it to a real endpoint later, set the `formEndpoint` prop on the page's `<script data-dc-script data-props="…">` tag (or in the Tweaks panel) to a URL that accepts `POST` JSON:

```json
{ "formEndpoint": { "default": "https://formspree.io/f/XXXXXXX" } }
```

Payload sent: `{ name, email, company, improve, message }`. Any 2xx response shows the success state; a failure asks the visitor to email `hello@equoren.com` instead. `contactEmail` changes the fallback address.

## Notes

- Content is deliberately free of company registration details, addresses, phone numbers, client names, statistics and testimonials. Equoren is presented as an early-stage validation project, not an incorporated company.
- Type: Newsreader + IBM Plex Sans (Google Fonts). Palette: warm off-white `#faf8f5`, charcoal `#1a1917`, bronze accent `#7f6130` / `#b79a63`.
