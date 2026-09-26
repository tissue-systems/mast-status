# mast-status

The Tissue Mast status page, served by GitHub Pages at
[status.tissue.systems](https://status.tissue.systems).

It lives here, off the Tissue fleet, so it stays readable when the thing it
reports on is down. The platform's own page is
[tissue.systems/status](https://tissue.systems/status).

## Who writes it

- A publisher on the Tissue monitoring host rewrites `index.html` every few
  minutes from the public Mast status API and the fleet's firing alerts, and
  pushes to `main` with a deploy key. Each render prints its time; the heading
  says "stale" once that time is more than ten minutes old.
- An operator writes `notice.txt` by hand. Its text appears under "From the
  operator" on every render until someone deletes it.

## Posting by hand

With the publisher running, edit `notice.txt` and push. The next render (within
two minutes) carries it:

```sh
git pull
$EDITOR notice.txt        # plain text, shown as written
git commit -am "notice: pages delayed" && git push
```

If the publisher itself is down, nothing will re-render, so edit `index.html`
directly as well: put the text in a `<div class="notice">` under the headline
and push. The render time in the page stays old, so the page still reads as
stale, which is true.

## Files

| File | What it is |
|---|---|
| `index.html` | The page. Plain HTML; the only script marks it stale. |
| `notice.txt` | Optional operator text. Absent or empty means no notice. |
| `CNAME` | `status.tissue.systems`, for the Pages custom domain. |
| `.nojekyll` | Serves the files as they are. |
