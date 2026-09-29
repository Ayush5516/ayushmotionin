# AGENTS.md

## Architecture

This is a single static HTML file (`index.html`) — no framework, no build step, no bundler. Tailwind CSS is loaded and configured directly via the CDN `<script>` tag in `<head>`, so styling changes can be made with utility classes without a build. Custom colors (`darkBg`, `cardBg`, `cardBorder`, `accentGold`) are defined in the inline `tailwind.config`.

## Key sections in index.html

- Header/nav with a mobile menu toggled by `#menu-btn` / `#mobile-menu`
- Hero section
- `#portfolio` — video categories, each embedding Google Drive `/preview` iframes
- `#pricing` — two rows of pricing cards (`.pricing-card`), each with an inline `onclick="selectPackage('<name>', <price>, '<cardId>')"`; `selectPackage()` in the inline `<script>` at the bottom of the file toggles the selected-state classes (`border-2 border-accentGold bg-accentGold/5` on the card, `bg-accentGold text-black font-bold` + "Selected ✓" text on its button) and updates `#selected-package-display`
- `#contact` — booking form; on submit, JS builds a WhatsApp message from the form fields and the currently selected package, then redirects to `wa.me`

## Conventions

- Keep all markup, styles, and behavior in `index.html` unless the file grows large enough to warrant splitting into separate CSS/JS files — this project intentionally has no build step, so any split must still work when served as static files with no transpilation.
- Pricing cards select via inline `onclick="selectPackage(name, price, cardId)"`, where `cardId` must match the card's own `id` attribute — the function looks the card up by that id to restyle it. Add all three arguments when adding a new card.
- The WhatsApp contact link (`https://wa.me/message/VVCNYHP3IFYKB1`) appears in the header, mobile menu, and footer — update all three if it changes. The booking form is an intentional exception: it redirects to a separate direct number (`fallbackWhatsAppNumber = "916001867854"` in the inline `<script>`) so booking messages land on that number specifically — update it there if it changes.
- Portfolio videos are embedded via Google Drive `/preview` iframe URLs. Replace the `src` values to swap videos; keep the `video-container-wrapper` div for consistent 16:9 sizing.

## Non-obvious decisions

- The hero photo points at a Google Drive image (`https://lh3.googleusercontent.com/d/<id>=w1000`) with an `onerror` fallback to `https://drive.google.com/uc?export=view&id=<id>`. Earlier attempts at embedding this same Drive file in other URL formats returned broken/black previews, so if this format also proves unreliable, fall back to a stock placeholder rather than retrying more Drive URL variants.
- `netlify.toml` publishes the repo root (`.`) since there is no build output directory.
