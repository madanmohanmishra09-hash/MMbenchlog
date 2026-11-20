# Work plan

A numbered outline for lab research. Objectives at the top, work items under them
(1.1, 1.2), sub-steps under those (a, b, c), and further levels below that — each
line carrying a status you can change as the work moves.

Statuses: **Ongoing**, **Repeat**, **Upcoming**, **Completed**, **Failed**. The
number and the text take the status colour, so a page of work reads at a glance,
and the bar under the project title shows the mix.

One HTML file, no build step, no server, no dependencies beyond two web fonts.

## Run it

Open `index.html` in a browser. That is the whole installation.

## Put it on GitHub Pages

1. Create a repository and push these files to the default branch.
2. **Settings → Pages → Build and deployment**, set *Source* to **Deploy from a
   branch**, pick that branch and the `/ (root)` folder, then save.
3. The site appears at `https://<username>.github.io/<repository>/` after a
   minute or two.

Every path in the app is relative, so it works from a project subfolder without
changes. `.nojekyll` stops GitHub's Jekyll step from touching the files.

On a phone, open that address and choose *Add to Home Screen* — the manifest and
service worker make it launch like an app and work offline.

## Where the data lives

In the browser's own storage (`localStorage`), under the key `workplan.v1`.
That means:

- Nothing is uploaded anywhere, and the plan is private to that browser.
- A plan saved on your laptop does **not** appear on your phone.
- Clearing site data, or a browser that aggressively prunes storage, erases it.

So use the toolbar buttons:

- **Back up** downloads the whole plan as a JSON file.
- **Restore** loads one back, replacing what is there.
- **Export CSV** gives a flat table for a report or a lab meeting.

`plan-backup.json` in this repository is a backup you can restore at any time.

## Using it

| Action | How |
| --- | --- |
| Add a sub-line under anything | hover the line, press **＋** (or **⋯ → Add sub-line**) |
| Keep adding | type, press **Enter**; the box stays open. **Esc** closes it |
| Rename | click the text |
| Status, date, notes | **⋯ → Details, notes, date** |
| Reorder | **▲ ▼**, or the same items in **⋯** |
| Change depth | **⋯ → Indent under line above / Outdent one level** |
| Bulk entry | **Paste a numbered list** under an objective |
| Focus on one status | click a band in the bar, or a label beneath it |

Numbering is always derived from position, never stored, so it stays correct
however you move things about.

**Paste a numbered list** reads indentation and markers: lines beginning `a.`
`b.` `c.` or a dash nest one level in, `i.` `ii.` `iii.` nest two, and leading
spaces work too. Numbers already in the text are stripped.

## Files

```
index.html             the whole application
starter-plan.js        data loaded on first run only; delete for a blank start
plan-backup.json       the same plan, restorable through the Restore button
manifest.webmanifest   installable-app metadata
sw.js                  offline cache
icons/                 app icons
.nojekyll              keep GitHub Pages from processing the files
```

## Changing it

Everything is in `index.html`: design tokens in the `:root` block at the top
(including the dark-mode values), the status list in the `STATUSES` array, and
the numbering scheme in `labelFor()`. Edit `CACHE` in `sw.js` to a new name when
you deploy a change, or returning browsers keep the old version.

## Licence

MIT — see `LICENSE`.
