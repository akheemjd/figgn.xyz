# Build a calculator tool page for figgn.xyz

## The site

figgn.xyz is a free online calculator site. Users get instant answers. We make money from Google AdSense. Every page must balance three priorities: **usability first**, **SEO**, and **ad revenue**.

## Design system (NO AI TELLS)

- **Font stack:** `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif` — native to every device. No Inter, no custom fonts.
- **Mono font for numbers:** `"SF Mono", "Cascadia Code", "Consolas", monospace`
- **Colors — Light mode:**
  - Background: `#f8f9fb`
  - Cards: `#ffffff`
  - Text: `#111111`
  - Secondary text: `#555555`
  - Input border: `#cccccc`
  - Primary button/accent: `#e65c00` (burnt orange, no gradients)
  - Result background: `#e7f5ec`
  - Result text: `#0d5c2e`
- **Colors — Dark mode:**
  - Background: `#131318`
  - Cards: `#1c1c24`
  - Text: `#e0e0e0`
  - Secondary text: `#999999`
  - Input bg: `#252530`
  - Input border: `#3a3a48`
  - Result background: `#0a3020`
  - Result text: `#4ade80`
- **Corners:** 4px. Not 8, not 12, not 16. 4px. Utilitarian.
- **Shadows:** One subtle shadow on cards: `0 1px 3px rgba(0,0,0,.08)`. Nothing else.
- **No:** glassmorphism, gradients, purple, indigo, icons, hero sections, symmetrical layouts, oversized whitespace.
- **Look:** Feels like a tool site from 2018. Trustworthy. Boring in the right way. Information-dense but readable.

## Dark/light mode

- Default: match `prefers-color-scheme`
- Toggle button top-right: text that says "Dark" or "Light"
- Persists in `localStorage` as `theme`
- All colors defined in CSS custom properties on `:root`
- No flash on page load

## Every page structure

```
DOCTYPE html5
<head>
  - title tag: "[Tool Name] Calculator — Free Online [Tool Name]"
  - meta description: ~155 chars, includes primary keyword
  - canonical URL: https://figgn.xyz/[tool-slug]/
  - og:title, og:description, og:url
  - Schema.org: WebApplication + HowTo + FAQPage structured data
  - All CSS inline in <style> (no external files for speed)
<body>

HEADER (thin bar, #e65c00 bg):
  - "figgn" wordmark left (links to /)
  - Dark/Light toggle right
  - NO navigation menu. Just home + toggle.

STICKY RESULT BAR (hidden until first calculation, then sticks to top):
  - Large result number in mono font
  - Supporting detail in smaller text
  - "Copy" button — copies result to clipboard, shows "Copied!" for 2 seconds

AD LEADERBOARD (728x90):
  - Background #f0f0f0, text "Advertisement", centered
  - max-width 728px, margin auto

TOOL AREA (white card):
  - Title: H1 = "[Tool Name] Calculator"
  - One-line description
  - Form inputs:
    - 56px height minimum on all inputs
    - inputmode="decimal" on number fields
    - Pre-filled with realistic default values
    - Results update ON EVERY KEYSTROKE (no Calculate button)
    - Tap presets where applicable (not dropdowns — actual buttons)
  - Secondary result details (if applicable)

AD RECTANGLE (300x250):
  - Background #f0f0f0, text "Advertisement", centered
  - Placed between tool and content sections

HOW TO USE (white card):
  - H2: "How to Use the [Tool Name] Calculator"
  - 3-4 numbered steps. Short, clear.

FORMULA / HOW IT WORKS (white card):
  - H2: "How It's Calculated"
  - The actual formula in plain English + math notation.
  - Real. Accurate. No fake formulas.

REFERENCE TABLE (white card, if applicable):
  - Real data. Real standards. No invented numbers.

FAQ (accordion):
  - H2: "Frequently Asked Questions"
  - 3-4 real questions with real answers.
  - Each <details> element with <summary>.
  - Schema.org FAQPage markup.

RELATED TOOLS:
  - H2: "More Free Calculators"
  - Links to 2-3 related tools on the site.
  - Small description under each link.

FOOTER:
  - Copyright, privacy link, home link.
  - Thin. Dark bg. Not a big footer.

AD STICKY FOOTER (mobile only):
  - 320x50 banner fixed to bottom of screen
  - Background #f0f0f0
  - Close button (X) that hides it for this session
