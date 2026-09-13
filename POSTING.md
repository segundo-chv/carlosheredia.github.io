# Posting checklist

The repo has three files that matter:

- `index.html` — the page. You rarely touch this.
- `posts.json` — the board contents. This is the one you edit.
- `CNAME` — maps heredia-viteri.org to this repo. **Never delete it.**

## Adding a post (about a minute)

1. Publish the piece on Substack. Copy its URL.
2. Open `posts.json` on github.com and click the pencil.
3. Add an entry at the TOP of the list:

   ```json
   { "cat": "shows", "score": 9, "title": "Your title here", "when": "Sep 2026", "url": "https://..." },
   ```

4. Delete the oldest entry if there are more than about nine.
5. Commit to `main`. The site updates within a minute.

### Field reference

| field   | what goes in it                                              |
|---------|--------------------------------------------------------------|
| `cat`   | `movies`, `shows`, `books`, `sport`, `food`, or `travel`      |
| `score` | a number 1 to 10, or `"ESSAY"` in quotes for unrated pieces   |
| `title` | the headline, in quotes                                       |
| `when`  | whatever you want displayed, e.g. `"Sep 2026"`                |
| `url`   | the Substack link, in quotes                                  |

JSON is stricter than HTML. Three things break it:

- a missing comma between entries
- a **trailing** comma after the last entry (allowed in JS, not in JSON)
- curly quotes instead of straight ones, if you drafted the title elsewhere

If an entry is malformed, the page drops that one entry rather than breaking.
If the whole file is invalid JSON, the board falls back to `FALLBACK` in
`index.html` and logs a warning in the browser console.

## Why it's a separate file

A scheduled job will eventually write `posts.json` automatically from your
Substack feed. Keeping it separate means that job can never damage the page
itself — the worst it can do is produce an empty board on a site that
otherwise still works.

## Other things you'll want to change

**The Currently strip.** Search for `CURRENTLY` in `index.html`. Three plain
sentences. Update every couple of weeks.

**Adding a drawing to a card.** Put the image in an `art/` folder, then add
`"art"` to that entry:

```json
{ "cat": "books", "score": 7, "art": "art/whatever.jpg", "title": "...", "when": "Aug 2026", "url": "..." },
```

Landscape images work best. Original artwork only — no recognisable
characters from anime, manga, film, or games.

**The Substack link.** Search `index.html` for `substack.com/@segundo4etapa`
and swap it for the publication URL once that exists.

## Two gotchas

**Opening index.html straight from your desktop shows an empty board.**
That's expected — browsers block `fetch` on `file://` URLs. It works fine
once served from GitHub Pages.

**`wrangler.jsonc` is still in the repo.** That's a Cloudflare config. Work
out whether Cloudflare or GitHub Pages is actually serving the domain before
you start publishing weekly, or you may push a change and see a stale page.

## Before the first deploy

Every entry currently in `posts.json` is made up. Replace them with real
posts, or empty the file to `[]`, which shows a clean "nothing here yet"
message instead.
