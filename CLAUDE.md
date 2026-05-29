# CLAUDE.md

Guidance for AI assistants working in this repository.

## What this is

`raptor-cool` is a **static, single-file marketing landing page** for the
**RAPTOR Sport** line of Thai herbal / cooling sport products (warming spray,
herbal roll-on, cooling spray). The copy is in Thai (`<html lang="th">`) and the
page is built for direct e-commerce conversion: flash-sale urgency, social
proof, and a LINE ordering link.

There is **no build system, no framework, and no package manager**. The live
page is plain HTML/CSS/JS that is served as-is and deployed to Vercel.

## Repository layout

| Path | Role |
|------|------|
| `index.html` | **The live landing page** (RAPTOR Herbal Roll-On). Self-contained: all CSS in one `<style>` block, all JS in `<script>` blocks at the bottom. This is the primary file you will edit. |
| `youtoo` | A **React/JSX component** (`RaptorIceLandingPage`) for an alternate "RAPTOR ICE COLD SPRAY" design. Uses `framer-motion`, `lucide-react`, and shadcn/ui (`@/components/ui/*`). It is a design reference / draft — there is **no React build, no `package.json`, and nothing imports it**. Do not assume it ships with the site. |
| `E8E82679-...png` | Main hero product image used by `index.html`. |
| `021FCB00-...png`, `E7BCE3F2-...png` | Optional extra frames for the 360° viewer (auto-detected at runtime; see below). |
| `Artboard 1_0.jpg` | Thumbnail used in the recommendation popup. |
| `RAPTORCOOL` | A JPEG image stored without a file extension (1200×1200). |
| `README.md` | Minimal (title only). |

## How `index.html` works

The page is one HTML file with three self-invoking JS modules (IIFEs) at the
bottom. When changing behavior, find the matching IIFE rather than adding new
script files:

1. **Flash-sale countdown** — drives every `[data-countdown]` timer. The end
   time is stored in `localStorage` under `raptorFlashSaleEnd` (6-hour window)
   and auto-resets when it expires.
2. **360° product viewer** (`#product360`) — pointer/touch drag and click cycle
   through product frames. It starts with one frame and **preloads optional
   images by filename** (`021FCB00-...png`, `E7BCE3F2-...png`,
   `product-front.png`, `product-left-front.png`); any that load successfully
   are added as extra rotation frames. To add an angle, drop the image in the
   repo and reference its exact filename in the `optional` array.
3. **Recommendation popup** (`#recommendPopup`) — slides in after 30 s. Product
   cards come from the `products[]` array inside the IIFE; add an object
   (`name`, `desc`, `price`, `link`, `image`) to add a card.

Other conventions in this file:
- **Inline everything.** Keep CSS in the single `<style>` and JS in the bottom
  `<script>` blocks. Do not introduce external CSS/JS files or a bundler.
- **Images are referenced by exact filename** (note filenames with spaces and
  no extensions). Keep references in sync when renaming assets.
- **Mobile-first responsiveness** is handled by `@media(max-width:900px)` /
  `700px` blocks and reordering with CSS `order`.
- **Analytics:** a Meta Pixel (`fbq`, id `462184846324554`) fires `PageView` in
  `<head>`. Preserve it unless asked to change tracking.
- **Conversion links** point to LINE: `https://lin.ee/X56gq67`. The
  recommendation popup also links to `https://raptor-sport.vercel.app/`.

## Development workflow

- **Editing:** modify `index.html` directly.
- **Testing:** there are no automated tests. Verify visually by opening
  `index.html` in a browser (or `python3 -m http.server` from the repo root so
  relative image paths and `localStorage` behave normally). Check both desktop
  and the ≤900px mobile layout, the countdown, the drag/click product viewer,
  and the 30 s recommendation popup.
- **Deployment:** the site is hosted on **Vercel** (`raptor-sport.vercel.app`).
  Pushing to the default branch is what ships changes; there is no separate
  build step.

## Git conventions

- Default branch is `main`. Work happens on short-lived feature branches that
  are merged via PR (history shows `codex/...` branches, e.g. small UI tweaks
  like "Adjust hero product image position").
- Commit messages are short, imperative, and describe the visible change
  (e.g. "Adjust mobile hero image position below product title").
- Keep commits focused; this is a presentation-layer repo, so most changes are
  copy, styling, layout, or asset swaps.

## Conventions for AI assistants

- **Match the existing style.** This is a hand-authored single-file site — do
  not refactor it into a framework, add a build pipeline, or split files unless
  explicitly asked.
- **Preserve the Thai copy and tone** (sport / premium / urgency). When editing
  marketing claims, keep the existing disclaimers (the herbal/efficacy sections
  already note results are subjective and not medical claims).
- **When adding product images or angles,** add the file and wire its exact
  filename into the relevant array (`optional` for the 360 viewer, `products[]`
  for recommendations).
- Treat `youtoo` as a design draft, not production code, unless told otherwise.
