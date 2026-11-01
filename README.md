# kitzis.org – Hugo site

Static Hugo version of kitzis.org (*Mind and Meaning*): a landing page and a privacy policy. No theme dependency; the layouts and CSS are in this repo.

## 1. Add the two files from WordPress (required)

Hugo can't build the download buttons without the book PDF and cover image. Put them here, keeping the same paths WordPress used so existing links to the PDF keep working:

```
static/wp-content/uploads/2022/02/Mind-and-Meaning.pdf
static/wp-content/uploads/2022/02/Screenshot_3-edited.jpg
```

Get them from the live site:
- https://kitzis.org/wp-content/uploads/2022/02/Mind-and-Meaning.pdf
- https://kitzis.org/wp-content/uploads/2022/02/Screenshot_3-edited.jpg

Do this **before** shutting down WordPress. If you have other uploads you want to keep, copy `wp-content/uploads/` from your WordPress host the same way.

## 2. Preview locally

Install Hugo (extended), then:

```
hugo server
```

and open http://localhost:1313.

## 3. Deploy on Cloudflare Pages

1. Push this folder to a GitHub (or GitLab) repo.
2. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**, and pick the repo.
3. Build settings:
   - Framework preset: **Hugo**
   - Build command: `hugo --minify`
   - Build output directory: `public`
   - Environment variable: `HUGO_VERSION` = a recent version, e.g. `0.169.0`
4. Deploy. You get a `*.pages.dev` URL to check first.
5. When it looks right: project → **Custom domains** → add `kitzis.org` (and `www` if you use it). If the domain's DNS is already on Cloudflare this is automatic; otherwise follow the prompts.
6. After DNS has switched and the site works, you can cancel the WordPress hosting.

(No Git? You can also use **Direct Upload**: run `hugo --minify` and upload the `public/` folder.)

## Notes

- **Old privacy link:** WordPress used `https://kitzis.org/?page_id=3`. The new URL is `/privacy-policy/`. Cloudflare Pages' `_redirects` file can't match query strings, so the old link will just land on the home page. If it matters, add a Cloudflare Redirect Rule matching URI query `page_id=3` → `/privacy-policy/`.
- **Privacy policy text:** migrated word for word. It mentions forms, comments and tracking, which a static site doesn't have; you may want to simplify it.
- **Other WordPress URLs:** the live site exposes only the home page and the privacy policy, so no other redirects are needed. If you had hidden posts or `/feed/` subscribers, tell me and I'll add them.
- `static/_headers` sets basic security headers and long caching for the uploaded files.
