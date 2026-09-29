# Updating content

All content is in `index.html`. The easiest way to find each piece is to search the file for the marker listed below (Cmd+F / Ctrl+F).

Several facts, such as the phone number and hours, appear in more than one place. Each section below lists every place that has to change together.

---

## Prices

Search for `id="prices"`.

Prices are split into four tabs (`id="p1"` to `id="p4"`), and each tab has one block per studio:

| Tab | Panel id |
|---|---|
| Lash extensions | `p1` |
| Refills | `p2` |
| Lamination & brows | `p3` |
| Sugaring & waxing | `p4` |

Inside each panel:

- `data-studio="wc"` holds Walnut Creek prices
- `data-studio="sf"` holds San Francisco prices

Each price is one row:

```html
<div class="prow"><span class="n">Classic</span><span class="d"></span><span class="p">$140</span></div>
```

To add a short description under the name, put it in `<small>` inside the name:

```html
<span class="n">Express extension<small>About 60% of lashes, a quick natural look</small></span>
```

**Also update:** the "from $…" starting prices in the **Services** section (search `class="from"`). They should match the cheapest option at either studio.

### Refills (Walnut Creek)

Walnut Creek refills have three time windows, each in its own block: `class="refill" data-d="7"`, `data-d="14"` and `data-d="21"`. The buttons above them (`id="refillTabs"`) switch between the blocks.

---

## Working hours and days

Hours appear in **five** places:

1. **Booking step 2:** the `data-days="…"` attribute on each studio button (search `data-group="location"`)
2. **Booking hint:** the default text of `id="daysHint"`, which should match the Walnut Creek `data-days`
3. **Contact card:** the `class="days"` paragraphs (search `class="contact-card"`)
4. **FAQ:** the "Where and when can I book?" answer
5. **Structured data:** `openingHoursSpecification` in the JSON-LD `<script>` in `<head>`. Use 24-hour `HH:MM` here (for example `"19:00"`) and full English day names (`"Monday"`).

On the page itself, write times in US format, for example `9 am–7 pm`.

---

## Phone number

Displayed as `+1 (628) 946-0049` and linked as `tel:+16289460049`. Search for `6289460049` to find every place: header menu, booking section, contact card, footer, mobile call button and JSON-LD.

Also update the `phone='…'` variable near the end of the `<script>`. It builds the SMS and WhatsApp links, and it holds digits only, with no `+`.

---

## Booking links (Square)

Each studio has its own Square booking URL.

| Studio | Search for |
|---|---|
| Walnut Creek | `LARVSCFZRRH7C` |
| San Francisco | `qwq980o9ct9uzz` |

Each URL appears in three places:

1. The "Where would you like to book?" popup (`id="bm"`)
2. The `id="bookOnline"` button (Walnut Creek only; it is the default)
3. The `URLS` object in the `<script>`

---

## Addresses

Each address appears in two places:

1. **Contact card:** the visible text and the "Get directions" Google Maps link. The link's `query=` is the URL-encoded address.
2. **JSON-LD:** `streetAddress`, `addressLocality` and `postalCode` in `<head>`

---

## Email and Instagram

- **Email:** search `mailto:`
- **Instagram:** search `lana_lash_studio_`. It appears in the contact card, the before/after section, the footer and `sameAs` in the JSON-LD.

---

## Gallery photos (Recent work)

Search for `id="grid"`. Each photo is one tile:

```html
<button class="tile" data-cat="ext" data-cap="Lash extensions">
  <img src="images/photo-11.jpg" width="860" height="1147" alt="Close-up of a natural lash extension set" loading="lazy">
  <figcaption>Lash extensions</figcaption>
</button>
```

| Field | Purpose |
|---|---|
| `data-cat` | Filter category: `ext` (Extensions), `lam` (Lamination), or both separated by a space (`ext lam`) |
| `data-cap` and `<figcaption>` | Caption; keep them the same |
| `width` / `height` | The photo's real pixel size, which prevents the page from jumping while it loads |
| `alt` | Short description for screen readers and search engines |

---

## Before / after slider

Search for `var BA=` in the `<script>`. Each entry is one client:

```js
{"b": "images/photo-16.jpg", "a": "images/photo-17.jpg", "c": "Lash lift"}
```

`b` is the before photo, `a` is the after photo, and `c` is the caption. Both photos of a pair need the same framing and aspect ratio.

The numbered buttons under the slider (`id="baTabs"`) need one button per entry, with `data-i` counting from 0.

---

## Reviews

Search for `id="qrail"`.

- The first four `<blockquote class="q">` are always visible.
- Reviews with `class="q more-q"` stay hidden until the visitor taps **Show all**.

If the total number of reviews changes, update the text "Show all 8 reviews" in **two** places: the button (`id="showAll"`) and the same text in the `<script>`.

---

## Adding a new image

1. Export it as JPEG, about 800–1200 px on the long side, with a file size under about 200 KB.
2. Save it as `images/photo-NN.jpg`, using the next free number.
3. Get its exact pixel size for the `width` and `height` attributes. On a Mac: `sips -g pixelWidth -g pixelHeight images/photo-NN.jpg`

---

## After any change

1. Check the page locally at phone width and desktop width. See "Running locally" in the [README](../README.md).
2. Update `<lastmod>` in `sitemap.xml` to today's date.
3. Commit and push to `main`. Vercel deploys automatically within about a minute.
