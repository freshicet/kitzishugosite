# Mind and Meaning

Source for [kitzis.org](https://kitzis.org/), the website for *Mind and Meaning: A Flight of Imagination, A Voyage of Discovery*, a book on the nature of mind, and perhaps the meaning of meaning. It is a science fiction story and an introduction to cognitive science.

The site is a small static site built with [Hugo](https://gohugo.io/) and hosted on [Cloudflare Pages](https://pages.cloudflare.com/). It has no theme dependency: the layouts and styles are all in this repository.

## Project layout

```
hugo.toml                 Site configuration
content/
  _index.md               Home page intro text
  privacy-policy.md       Privacy policy page
layouts/
  index.html              Home page (cover image, intro, PDF buttons)
  _default/baseof.html    Shared page shell and footer
  _default/single.html    Template for inner pages
  404.html                Not-found page
static/
  css/style.css           Site styles
  fonts/                  Karla font files (self-hosted, with license)
  wp-content/uploads/     Cover image and book PDF
  _headers                Cloudflare security and caching headers
```

## Running locally

Install [Hugo](https://gohugo.io/installation/) (any recent version), then from the repository root:

```
hugo server
```

and open http://localhost:1313. To build the site into `public/`:

```
hugo --minify
```

## Editing

- **Intro text:** `content/_index.md`
- **Privacy policy:** `content/privacy-policy.md`
- **Page layout and buttons:** `layouts/index.html`
- **Colors and sizes:** `static/css/style.css`. The `SIZE SETTINGS` block at the top controls text size, button size, cover image width and page width.
- **Book PDF and cover image:** replace the files in `static/wp-content/uploads/2022/02/`, keeping the same file names. The paths match the old WordPress site, so existing links to the PDF keep working.

## Deployment

The site deploys automatically from this repository using Cloudflare Pages. Every push to the main branch triggers a new build.

Cloudflare Pages settings:

| Setting | Value |
|---|---|
| Framework preset | Hugo |
| Build command | `hugo --minify` |
| Build output directory | `public` |
| Environment variable | `HUGO_VERSION` (optional; pins the Hugo version) |

## Credits

- Built with [Hugo](https://gohugo.io/).
- Typeface: [Karla](https://fonts.google.com/specimen/Karla), self-hosted under the SIL Open Font License (see `static/fonts/KARLA-LICENSE.txt`).
