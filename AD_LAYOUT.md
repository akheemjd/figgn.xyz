# figgn.xyz — ad layout system

One slot system, shared across every page. Placement and timing live here; the
visual redesign should only touch colours and spacing, never this structure.

## Principles

1. **Nothing sits between a visitor and their answer on mobile.** People arrive
   from search wanting a number. The first ad appears to a satisfied user.
2. **Every slot reserves its height before it fills.** Zero layout shift. CLS is
   a ranking factor, and ranking is the whole business.
3. **Slots fill lazily**, 600px before entering the viewport. Nothing off-screen
   costs load time.
4. **The sticky unit is earned, not automatic.** It appears after the visitor
   engages — first keystroke, or scrolling past half a screen.

## Placements

| Slot | Size | Position | Shows on |
|---|---|---|---|
| `leaderboard` | 728×90 | Above the tool card | Desktop only (≥768px) |
| `primary` | 300×250 / 336×280 | Directly below the tool card | All |
| `secondary` | 300×250 / 336×280 | Above the FAQ | All |
| `stickyAd` | 320×50 | Fixed bottom | Mobile only (≤640px), after engagement |

The homepage carries **one** `secondary` unit below the catalog, no sticky and no
leaderboard. It is a navigation page — ads above the links cost more in bounce
than they earn.

`primary` is the money slot. It sits at the moment of highest intent: the
visitor has their answer and their attention is still on the page.

## Markup

```html
<aside class="adwrap" data-ad="primary">
  <span class="adlabel">Advertisement</span>
  <div class="adslot" data-size="300x250 / 336x280"></div>
</aside>
```

## Going live with AdSense

Two edits, both inside the ad controller script:

1. Replace the `.adslot` contents with your `<ins class="adsbygoogle">` unit.
2. Uncomment the `adsbygoogle.push({})` line inside `fill()`.

Load the AdSense script itself with `async` after first interaction, not in
`<head>` — it is the single heaviest request on the page.

## Before launch

- `/privacy/` must exist and disclose cookie and ad-personalisation use. AdSense
  approval depends on it.
- Keep 24px of clear space around the Copy button and every preset row. Ads
  adjacent to controls generate accidental clicks, and accidental clicks
  generate invalid traffic strikes.
- Dismissal of the sticky unit persists for the session via `sessionStorage`.
  Do not extend it to `localStorage` — a permanently dismissed unit earns nothing.

## Not yet done

- Responsive AdSense units rather than fixed sizes.
- Slot-level revenue tracking to confirm `primary` outperforms `leaderboard`,
  which is the assumption this layout is built on.
