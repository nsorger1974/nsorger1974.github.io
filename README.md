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
- Session sign-up → "Zoom link — Morocco info session, September 15"

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

## The information session (removed)

The home page and the Morocco page used to carry a panel announcing a Zoom
information session. That date has passed, and the panel, its hero button, and its
now-unused CSS have been removed from both pages.

If you run another info session in the future, the cleanest approach is to rebuild
this as a small self-contained section (heading, date/time, one paragraph, and a
sign-up form posting to Formspree) rather than reviving the old one, since the old
markup is now gone from the page templates.

## Pricing and inclusions

What's included and excluded appears in two places: the "What's included, and what
isn't" question in the About page FAQ, and the "Good to know" list on the Morocco
page. If the terms change, edit both.

Morocco pricing and terms live in a dedicated section on the Morocco page — search
for `id="booking"`. In short: $3,900 for the 7-day option, $4,500 for the 9-day, both
double occupancy; $1,000 single supplement; $750 deposit due November 1, 2026;
balance January 15, 2027; fully refundable through December 1, 2026 and
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

## SEO metadata (added September 2026)

Every page now carries a full set of search and social metadata:

- **Title & description** — tuned per page around your target search terms
  (women's travel, women's adventure travel, midlife travel, second act, empty
  nest, freedom to travel, plus the destination and city names).
- **Meta keywords** — included for completeness, though modern search engines
  largely ignore this tag; the real SEO value is in the titles, descriptions,
  and the visible page copy itself, which already reads naturally.
- **Open Graph + Twitter Card tags** — control how the site looks when a link
  is shared on Facebook, Slack, iMessage, LinkedIn, or X. Each page now has a
  proper 1200×630 preview image (see `images/social/`) instead of showing
  nothing.
- **Structured data (JSON-LD)** — a `TravelAgency` schema on the home page and
  a `TouristTrip` schema on the Morocco page, which helps Google understand
  what kind of business this is and can support richer search results over
  time.
- **`robots.txt` and `sitemap.xml`** — new files at the root of the site,
  telling search engines the site is open to indexing and listing all five
  pages. Neither existed before.

### One thing to do once the domain is live

**Submit the site to Google Search Console** (search.google.com/search-console
— free) and Bing Webmaster Tools. Verify ownership of certainlatitude.com, then
submit `https://www.certainlatitude.com/sitemap.xml`. This is what actually
gets a new site crawled and indexed — none of the metadata above does that on
its own, it only controls how the site is *described* once found.

### A note on "travel for moms"

That phrase is included in the keywords and description as requested, but
it's worth knowing it can point in two different directions: people searching
it are often looking for family trips *with* children, which is the opposite
of what Certain Latitude offers. It's included because you asked for it and it
isn't wrong for an empty-nester audience — just be aware it may also attract
some searches for the wrong kind of trip.

### If a page's core content changes

The title, description, and keywords are written by hand for the copy as it
stood in September 2026. If the itinerary, dates, or positioning change
significantly later, these should be revisited so they still match what the
page actually says.

## Venmo payment (added September 2026)

A "Pay Here" link now sits at the end of the main navigation bar on every page,
linking to `morocco.html#pay` — it jumps straight to the Venmo card. The nav is
duplicated across all five HTML files (there's no shared template anymore), so
if you ever change this link, update it in all five.


The Morocco page's "Prices, payment and refunds" section ends with a "How to pay"
entry and a "Pay via Venmo" button, pointing to `@certainlatitude`. Search for
`venmo-pay` in `morocco.html` to find it.

This is deliberately button-only, with no QR code displayed publicly, and the
copy asks people to confirm their place with Nicole before paying — the site
isn't meant to be a self-serve checkout. Two QR image files
(`images/venmo-qr.png` and `@2x`) are still in the images folder, unused, in
case you want to bring the QR code back later.

If the Venmo account ever changes, update the link on the button — search for
`venmo.com/code` in `morocco.html` — and regenerate the QR files if you restore
the image version.

There is also a ready-to-send email template for confirmed travelers, with the
same payment link and a reminder about the deposit deadline and the required
Venmo note. Ask Claude to regenerate it if the price, dates, or terms change.

**Worth knowing, not a website issue:** Venmo's personal accounts are built for
paying friends, not for collecting business payments — there's a separate "Venmo
for Business" profile type with its own terms. Using a personal account for
$750 client deposits works in practice, but it means payments carry none of the
buyer protection a real payment processor (Stripe, Square, PayPal Business) would
offer, and there's no automatic record tying a payment to a specific traveler or
trip — that's why the page asks people to put their name and "Morocco deposit" in
the Venmo note. Worth keeping a manual list of who's paid, since Venmo won't do
that bookkeeping for you.

## Site search

Every page has a search button in the main nav (magnifying-glass icon, next to
"Make a Payment") that opens a search overlay. Type a few letters and it filters
an on-page index — no server, no external service, works the moment the site is
live. Press `/` anywhere on the page to open it, `Esc` to close it, arrow keys to
move between results, `Enter` to go to the top one.

**How it works:** each page carries an identical copy of `SEARCH_INDEX`, a
JavaScript array near the bottom of the file — search for `var SEARCH_INDEX` to
find it. Each entry is `[title, url, snippet, page label, isSubsection]`. Typing
scores matches by where the text hits (title match ranks above a snippet match)
and shows the best 8.

Itinerary days (Morocco) and FAQ answers (About) can be linked to directly and
will auto-expand when opened this way — search for `openAccordionTarget` to see
how. If you add a new day or FAQ question, give its `<article class="day">` a
unique `id`, then add a matching entry to `SEARCH_INDEX` with a URL like
`morocco.html#your-new-id`.

**Because the index is duplicated across all five files, any change has to be
made five times** — there's no shared template to edit once. Keep them in sync
by checking after any edit:

```
grep -c "your search text" index.html morocco.html argentina.html uzbekistan.html about.html
```

All five counts should match.
