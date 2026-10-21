# Shelf

Every book you finished, on your phone: cover, the day you finished it, a mark from 1 to 10,
your notes and a line worth keeping.

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

One file, no dependencies, no build step: `index.html`. Same look and the same motion helpers as
[EPFL Focus](https://github.com/Bubagna/epfl-focus). Bump `CACHE` in `sw.js` and `BUILD` in
`index.html` whenever a file changes, or phones keep the old copy.
