# kindling.lantern.io

The website for [Kindling](https://github.com/getlantern/kindling), Lantern's library for getting
small amounts of data through censoring firewalls: one static `index.html` with no build step,
served by Cloudflare Pages.

Cloudflare Pages builds this repository straight from GitHub: every push to `main` deploys it, with
no build command and the repository root as the output directory. `_headers` sets the response
headers.

To preview locally, open `index.html` in a browser, or run `python3 -m http.server`.

The site moved here from `site/` in [getlantern/kindling](https://github.com/getlantern/kindling),
with its history.

`404.html` is the not-found page. Without it, Cloudflare Pages answers every path that has no
file with `index.html` and a 200, so crawlers see a copy of the home page at every broken link.

## The FAQ and structured data

The FAQ lives in `tools/faq.py`, which writes both the visible FAQ section and the schema.org
`FAQPage` markup into `index.html`, so the two always say the same thing. To change a question or
answer, edit the list there and run `python3 tools/faq.py`. The same script writes the rest of the
JSON-LD graph (`Organization`, `WebSite`, `WebPage`, `SoftwareSourceCode`). Check every answer
against the README and code in getlantern/kindling before changing it.

`og.png` is the 1200×630 link-preview image, a screenshot of `tools/og.html`. `robots.txt` and
`sitemap.xml` point crawlers at the one page; update the sitemap's `lastmod` when the page changes.
