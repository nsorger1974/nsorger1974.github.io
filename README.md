# Certain Latitude — website

Five pages, no build step, no dependencies. Every file is self-contained (CSS and
JavaScript are inlined), so you can upload the folder to any host as-is.

```
index.html        Home — hero, the three tabs, latitude scale, Morocco feature, interest list
morocco.html      Morocco 2027 — full day-by-day itinerary, flights, good to know
argentina.html    Argentina 2028 — preview, marked "in development"
uzbekistan.html   Uzbekistan 2029 — preview, marked "in development"
about.html        About, how we travel, founder, FAQ
```

## Putting it live at certainlatitude.com

Any static host works. The simplest options:

- **Netlify** — drag this folder onto app.netlify.com/drop, then add the domain
  under Site settings → Domain management.
- **Cloudflare Pages** or **GitHub Pages** — push the folder to a repo and point
  the domain at it.
- **Traditional hosting** — upload the five `.html` files to the web root.

`index.html` is the home page automatically. Nothing else to configure.

## The forms

Two forms: the interest list (bottom of every page) and the information session
sign-up (home page and Morocco page). Both post to Formspree at
`https://formspree.io/f/mvkplkdq`, and submissions arrive at certainlatitude@gmail.com.

**Before the first real sign-up**, submit each form once yourself. Formspree holds
delivery until you confirm the address, and the confirmation email is triggered by
the first submission.

### How it works

Each form has `action="https://formspree.io/f/mvkplkdq" method="POST"` on the tag
itself, and the site's JavaScript intercepts the submit and sends it in the
background so the visitor stays on the page and sees a thank-you where the button is.

If the JavaScript ever fails to load, the browser falls back to posting the form
normally — it still reaches you, the visitor just lands on a Formspree page instead.
Nothing is lost either way. That is why the `action` attribute matters; don't remove it.

### Telling the two forms apart

Both post to the same endpoint, so each carries a hidden `_subject` field that sets
the email subject line:

- Interest list → "Certain Latitude — interest list"
- Session sign-up → "Zoom link — Morocco info session, August 30"

Filter or label on those in Gmail and the two streams stay separate. If you would
rather have them fully separate, create a second form in Formspree and swap the
endpoint on the session form only — search for `session__form`.

Each form also has a hidden `_gotcha` field. It is a spam trap: real people never
see it, bots fill it in, and Formspree silently discards those submissions.

### Changing the message people see

The thank-you and error wording lives in the script at the bottom of each page,
in the block beginning `data-fs-form`. Search for "Nicole will be in touch".

### Upgrading the plan

The free tier covers 50 submissions a month. If the Zoom session drives more than
that, submissions above the limit are held rather than lost, but you will not be
emailed until you upgrade.

## Photographs

`images/chefchaouen-door.jpg` is the hero image on the home page — your photo of
the turquoise door in the blue medina, cropped to 4:5 and saved at two sizes so
phones don't download the large one.

## Photographs of Nicole

`nicole-chefchaouen.jpg` is on the About page, in the "Latitude, both ways" section
— you beside the blue door in Chefchaouen.

The headshot lives in `images/` in three sizes: `nicole-sorger.jpg` (900px
wide, the default), `nicole-sorger@2x.jpg` for retina screens, and
`nicole-sorger-square.jpg` for social profiles. It appears in the "Meet our
founder" tab on the home page and in the founder section of the About page.

Keep the `images/` folder next to the HTML files when you upload — that's what
the `src="images/…"` paths point to.

## Photographs on the Morocco page

All five of your Morocco photographs are placed:

- `chefchaouen-panorama` &mdash; the wide band under the trip facts, the view toward
  the Spanish Mosque
- `chefchaouen-stairs`, `fes-brass-gates`, `fes-pigments`, `tangier-souk`,
  `marrakech-couscous` &mdash; the five-photo gallery near the bottom of the page

To swap one, replace the file in `images/` keeping the same name, or edit the
`<img src>` inside the matching `<figure class="shot">`. Gallery photos are cropped
to 4:5 portrait; the band is 21:9. Each has a normal and an `@2x` version, and the
browser picks the right one automatically.

## The destination globes

`images/globe-argentina.svg` and `globe-uzbekistan.svg` sit in the hero of each of
those pages: a real orthographic projection centred on the city, with the country
filled, the city's own parallel drawn through it in orange, and an X on the spot.

They are drawn from Natural Earth coastline data rather than traced, so the
geography is accurate. Vector, so they stay sharp at any size, and the captions are
converted to outlines &mdash; an SVG loaded through `<img>` can't reach the web fonts,
so live text would have fallen back to a default face.

When you have photographs from either country, a `<figure class="shot">` gallery can
be added to those pages the same way as on Morocco. The globes can stay in the hero.

## The information session

The home page and the Morocco page both carry a panel announcing the Zoom session on
Sunday, August 30 at 5:00 PM Pacific, with a short sign-up form. Search either page
for `id="session"` to find it. The two copies are identical — edit both.

Like the main interest form, it opens the visitor's email app with a message ready
to send to certainlatitude@gmail.com — so sign-ups arrive as ordinary emails.

**After the session, delete this block from both pages**, or the site will keep
advertising a date that has passed. Remove the whole `<section ... id="session">`
element and the "Info session · Aug 30" button in each hero.

## Pricing and inclusions

What's included and excluded appears in two places: the "What's included, and what
isn't" question in the About page FAQ, and the "Good to know" list on the Morocco
page. If the terms change, edit both.

Morocco pricing and terms live in a dedicated section on the Morocco page — search
for `id="booking"`. In short: $3,900 for the 7-day option, $4,500 for the 9-day, both
double occupancy; $1,000 single supplement; $750 deposit due October 15, 2026;
balance January 6, 2027; fully refundable through December 1, 2026 and
non-refundable after.

Shorter versions of the same facts appear in the About page FAQ (three separate
questions) and in the Morocco facts strip near the top of the page. If terms change,
check all of them.

The travel-insurance link points to `https://www.squaremouth.com/22602`. If that
becomes a different link, search for `squaremouth` and you'll find both instances.

## Editing text

Open any file in a text editor and search for the sentence you want to change.
The pages are plain HTML — no framework, no templates.

A few things worth knowing:

- **The four taglines** appear at the top of all three trip pages, in the dark blue
  band. They are identical in each file, so change all three if you edit them.
- **Dates and prices.** Argentina and Uzbekistan deliberately say "in development"
  and carry a note explaining that nothing is bookable yet. Pricing is not stated
  anywhere — the FAQ says final pricing goes to the interest list first.
- **The latitude scale** on the home page is drawn to real coordinates. If you
  change a destination, the pin position is the `y` value in the SVG, calculated as
  `34 + (45 − latitude) / 90 × 500`. Southern latitudes are negative.

## Design notes

- **Color** comes from the Morocco flyer: Chefchaouen blue `#3C86C6`, cobalt
  `#1B5FA8`, deep navy `#0E2A4A`, pale sky `#A9CDE8`, near-white `#F6F8F9`. The one
  warm accent is orange `#C7601A` — the same color as the center of the khatem logo
  — used for the primary buttons, the equator line, day numbers, and small markers.
  Its light counterpart `#EBB587` handles small orange text on navy. Both are defined
  once as `--brass` and `--brass-lt` at the top of every page's stylesheet, so
  changing the accent everywhere is a two-line edit.
- **Type** is Instrument Serif for display, Karla for body, and Josefin Sans for
  the small uppercase labels — nav, dates, coordinates, section eyebrows. All three
  load from Google Fonts, with system fallbacks if that ever fails. Josefin runs
  light with a small cap height, so every label is set at weight 600 with a size
  bump; that adjustment lives in one block at the end of the stylesheet.
- **Ground color** is a warm gray (`#EDE8E0`), with a deeper warm gray (`#E3DCD1`)
  for alternating bands and white for cards. The background texture is the khatem
  star from the logo, tiled and set at around 10% opacity.
- **The eight-pointed star** in the background texture is the khatem, the tile motif
  that runs from Moroccan zellige to Uzbek ceramics — which is part of why those two
  destinations sit together on this site.
- Accessible by default: keyboard navigation throughout, visible focus rings, real
  tab and accordion semantics, and animation switched off for anyone whose system
  asks for reduced motion.

## Logos

The `logos/` folder holds three identity directions; open `logo-sheet.html` to compare
them. The chosen mark is **B, the khatem** — the eight-pointed zellige star, with a
medium-dark orange center (`#C7601A`).

It is already wired into the site: the star appears next to the wordmark in the
header, above the wordmark in the footer, and as the browser tab icon. All of that
is drawn in code, so there is no image file to upload and nothing to break.

To swap in a different concept, search any `.html` file for `brand__mark` (header)
or `footer__star` (footer) and replace the `<svg>…</svg>` block.
