# standardbeagle.github.io

The user site for `standardbeagle.github.io` — a project index, and the host-wide files that only
this repository can serve.

## Why this repository exists

Every Standard Beagle project site is a GitHub Pages **project** site, served as a subpath of this
one host: `standardbeagle.github.io/tman/`, `/agnt/`, `/mcp-tui/`, and so on. Some things are read
only from the **domain root**, and the domain root belongs here:

| file | why it cannot live in a project repo |
| --- | --- |
| `robots.txt` | Crawlers read it only from `/robots.txt`. A copy at `/tman/robots.txt` is ignored. |
| `sitemap.xml` | Can live anywhere, but a single index at the root is the one URL to submit for every project at once. |
| `404.html` | The user site's 404 page is served for unmatched paths across the whole host, including paths under a project that has no 404 of its own. |

Before this repository existed, `https://dev.standardbeagle.com/` returned **404**, so none of the
above was servable for any of the eleven project sites and the one URL they all share was an error
page.

## Layout

```
index.html          project index, grouped by area
404.html            host-wide 404
robots.txt          allows everything, points at the sitemap index
sitemap.xml         sitemap index
sitemap-sites.xml   the root page plus every project home page
favicon.svg
```

No build step and no dependencies — GitHub Pages serves this directory as-is from `main`.

## Adding a project

1. Add a card to `index.html` in the right section.
2. Add its home page to `sitemap-sites.xml`.
3. If the project publishes its own `sitemap.xml`, add it to `sitemap.xml` as well. If it does not,
   step 2 is enough for it to be discovered.
4. Add it to the list in `404.html`.

**Link only what actually serves.** A hub pointing at 404s is worse than no hub, because it is
trusted. Check before adding:

```sh
curl -s -o /dev/null -w '%{http_code}\n' -L https://dev.standardbeagle.com/<project>/
```

`brummer` has Pages enabled but serves 404, so it is deliberately not linked here. Add it once it
deploys.
