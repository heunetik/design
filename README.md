# design

Shared styling for heunetik apps, served as plain CSS from `https://design.heunetik.dev/v1/`. No build step, no framework: any app that can load a stylesheet can use it.

## Use

Link the files first, before any app stylesheet. Only `tokens.css` is required.

```html
<link rel="stylesheet" href="https://design.heunetik.dev/v1/tokens.css">
<link rel="stylesheet" href="https://design.heunetik.dev/v1/base.css">       <!-- optional -->
<link rel="stylesheet" href="https://design.heunetik.dev/v1/components.css"> <!-- optional -->
```

| File | Contents |
|---|---|
| `tokens.css` | Fonts and `--heu-*` custom properties: color, type, space, radius, depth, motion, focus. Theme switching. |
| `base.css` | Element defaults: body, headings, links, focus ring, text fields, select, checkboxes, radios, details, tables, dialog. |
| `components.css` | Opt-in `.heu-*` classes: card, kicker, button, segmented, toolgroup, chip, meter, callout, menu, sr-only. |

Depth tells users what they can do: a 2 to 3px bottom edge means pressable (buttons, select, toggle chips), a 1px edge means a resting surface (callouts, status chips), and a sunken well holds input or a value (fields, tracks). Large containers (cards, dialogs, menus) are the exception: they keep the 3px edge, which reads as a panel at that size, not a key. Keep new elements to the same rule.

Everything sits in the `heu` cascade layer, declared by `tokens.css`. Any app style loaded afterwards, layered or not, wins without extra specificity.

The site root (`public/index.html`) shows every token and component with its markup. Snippets are read from the live previews, and the token sections are read from `tokens.css`, so a new token appears there without touching the page.

## Theme

Follows the system by default. `data-theme="light"` or `data-theme="dark"` on `<html>` forces one. Colors use `light-dark()`, so there is no dark-mode code anywhere else.

## Versions

`/v1/` changes in place: additions and fixes reach every app on its next load. Renaming or removing a token or class is breaking and goes to a new `/v2/` folder, so each app moves when it is ready.

## Develop and deploy

```sh
npm install
npm run dev     # http://localhost:8787/v1/tokens.css
npm run deploy  # Cloudflare, design.heunetik.dev
```
