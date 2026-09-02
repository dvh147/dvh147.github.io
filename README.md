# dvh147.github.io

Personal academic website for Dennis Verhoeven. Plain HTML and CSS, no build step, no
dependencies. GitHub Pages serves the files exactly as they are in this repository.

Live at <https://dvh147.github.io>.

## Layout

```
index.html            Homepage ("About")
research.html         Journal articles, working papers, work in progress
policy.html           Policy reports
teaching.html         Courses, workshops and supervision
writing.html          Index of posts, and a pointer to Research Notes
404.html              Shown for any URL that does not exist
posts/                One HTML file per post
assets/style.css      All styling for the whole site
assets/files/         CV, portrait, institutional logos, post images
.nojekyll             Tells GitHub to serve the files as-is
```

The layout is a fixed sidebar on the left (name, photo, role, navigation, the
three institutional logos) with the content on the right. Below 928px it stacks
into one column.

The separate `research-notes` repository is published at
<https://dvh147.github.io/research-notes/> and is linked from this site. It stays its own
repository, so the agent that writes those notes keeps working unchanged.

## Editing

Every page is a single self-contained HTML file. Open it, change the words, save. The
`<aside class="sidebar">` block is repeated in each file — if you add or rename a page,
update that block in all seven, and move the `aria-current="page"` marker to the right link.

Colours, fonts and spacing all live at the top of `assets/style.css` as variables. Change a
value there and the whole site follows. The accent is SKEMA's own red, `#e7433c`, darkened
to `#c9352c` for link text so it clears the WCAG AA contrast threshold on white; the
brighter original is kept for the rules under headings.

The logos were cut from `Dropbox (Personal)/Templates/2025logos.png` and the portrait from
`ProfilePics/SKEMA-Small-file.jpg`. In dark mode the logos sit on a white chip, because the
SKEMA and LSE marks are near-black and would otherwise disappear.

Spots that need your attention are marked in the HTML with `<!-- EDIT: ... -->` comments.

## Previewing before you publish

Root-relative links (`/research.html`) do not resolve when opening files directly from disk,
so run a local server from this folder:

```
"C:\Users\dennis.verhoeven\AppData\Local\anaconda3\python.exe" -m http.server 8000
```

Then open <http://localhost:8000>. Stop it with Ctrl+C.

## Adding a post

1. Copy `posts/2026-09-02-a-first-post.html` to `posts/YYYY-MM-DD-your-slug.html`.
2. Change the `<title>`, the `<h1>`, the date, and the body text.
3. Open `writing.html` and add an entry between the `<!-- POSTS:START -->` and
   `<!-- POSTS:END -->` markers, newest first.
4. Commit and push.

## Publishing

```
git add -A
git commit -m "Describe the change"
git push
```

The site rebuilds within about a minute.

## Adding the custom domain later

Once you have bought a domain, this takes about ten minutes plus DNS propagation:

1. Create a file named `CNAME` in this folder containing only the domain, e.g.
   `dennisverhoeven.com`. Commit and push.
2. At the registrar, point the domain at GitHub. For an apex domain, four `A` records:
   `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`; and four
   `AAAA` records: `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`,
   `2606:50c0:8003::153`. Add a `CNAME` record for `www` pointing to `dvh147.github.io`.
   Check these against GitHub's documentation at the time, since the addresses can change.
3. In the repository settings under Pages, enter the domain and tick **Enforce HTTPS** once
   the certificate has been issued.

Nothing on the site needs to change: all internal links are root-relative, so they keep
working under the new domain, and `research-notes` moves to `yourdomain.com/research-notes/`
automatically.

## A note on Dropbox

This folder sits inside Dropbox, which syncs the `.git` directory as well. That is usually
fine, but avoid running git commands while Dropbox is mid-sync, and never have the same
repository open on two machines at once.
