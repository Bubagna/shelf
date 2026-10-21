# Shelf

Every book you finished, on your phone: cover, the day you finished it, a mark from 1 to 10,
your notes and a line worth keeping. A second list, **To read**, keeps the books you mean to read;
when you finish one, a tap moves it to the shelf.

It looks like an old wooden library: walnut boards, books standing on planks, a wax seal with the
mark, parchment pages for the details. A darker *candle* light follows the phone's dark mode.

Type a title or an author, in Italian or English, and Shelf finds the book: cover, blurb,
first-edition year and page count are filled in for you. Tap it, give it a mark, done.

## Install it

Open the page in Safari on iPhone, then **Share → Add to Home Screen**. After the first load a
service worker keeps the app on the phone, so the shelf opens with no network (searching for a
new book still needs one).

## Where the data comes from

Every search goes to three catalogues at once and merges the answers into one row per book:

| Source | What it gives |
|---|---|
| Apple Books, Italian store | covers, blurbs in Italian, genres |
| Apple Books, US store | the same for English editions |
| Open Library | first-edition year, page count, books Apple does not sell |

Google Books is not used: without an API key it answers `429` for everyone.

## What it stores

Books live in `localStorage` (`shelf.v1`), covers in IndexedDB as small jpegs, all on the phone.
Nothing is uploaded. Settings → Export writes one JSON file with every book and every cover;
Import merges a file back in.

## Hacking on it

One file, no dependencies, no build step: `index.html`. Fonts (IM Fell English, EB Garamond) are
bundled in `fonts/`; the wood grain is SVG noise drawn by the browser, so there are no image assets. Bump `CACHE` in `sw.js` and `BUILD` in
`index.html` whenever a file changes, or phones keep the old copy.
