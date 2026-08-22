# Mantech Media — website

Plain HTML, CSS and vanilla JS. No build step, no framework, no server —
every page works straight off disk or from any static host.

## How to post a new story (do this — nothing else)

1. Open **`data/articles.js`**.
2. Copy the template block at the top of the file (between "COPY FROM
   HERE" and "COPY TO HERE").
3. Paste it into the `articles[]` list, fill in your title/text/category.
4. Save.

That's it. No build step. The story appears automatically on the
homepage, its category page, search, and its own article page. The
site currently ships with 5 articles per category (News, Apple,
Devices, Business, South Africa) written as real, full-length reads —
publish over them or add more using the same template.

## Page map

```
index.html                        Homepage
pages/category.html?category=X    News / Apple / Devices / Business / South Africa
pages/article.html?id=X           One story (X = the "id" field in data/articles.js)
pages/about.html                  About Mantech Media
pages/studio.html                 Mantech Studio — the company/services side (not news)
pages/work.html                   Studio project showcase
pages/contact.html                Contact (CTO: mabasaamu0@gmail.com)
pages/privacy.html                Privacy policy + editorial accuracy note
```

The header nav includes a "Studio" link (subtle outlined pill) alongside
the news categories, and the homepage's Business section includes one
quiet, honestly-labeled Mantech Studio card among the story cards —
that's the site's one native promo slot, in `js/main.js`.

## How Subscribe works

Clicking "Subscribe" opens the visitor's own email app, pre-addressed to
the CTO's inbox with their email in the body — there's no backend, so
this is how the address actually reaches you today. Read the comment
block above the `SUBSCRIBE` section in `js/main.js` for the full
explanation, including how to swap this for a real email service
(Mailchimp, Buttondown, ConvertKit all offer a free tier and a
copy-paste form) once you're ready to send automatically instead of by
hand.

As a bonus, subscribing also sets a flag in that browser's
`localStorage`, so a returning subscriber sees "3 new stories since your
last visit" under the form — this part never leaves their device.

## Security & SEO

- Every page ships a strict Content-Security-Policy (safe to do since
  the site loads nothing external — no fonts, no CDNs, no third-party
  scripts).
- The one place user input gets echoed back (search results) is escaped
  before insertion — see `escapeHTML()` in `js/main.js`.
- `robots.txt` and `sitemap.xml` are at the project root and list every
  page and article.
- Favicons ship in both light and dark variants (`prefers-color-scheme`)
  so the logo stays visible in a dark browser tab bar.

## Code layout

```
data/articles.js          All story content lives here — the only file
                           you should need to touch to publish something.
css/style.css              All styling, one file.
js/main.js                 Runs on every page: date, menu, search, Subscribe.
js/category.js              Runs only on pages/category.html.
js/article.js                Runs only on pages/article.html.
assets/icons/                 Logo marks + favicons (light + dark), generated
                               from the source logo.
assets/images/                 og-image.jpg (social share) + 5 shared category
                                placeholders (fallback option — see the
                                template comment in data/articles.js).
assets/images/articles/         One unique placeholder image per story,
                                 named to match its "id".
```

Each JS file has a comment block at the top explaining what it's
responsible for — start there if something needs changing.
