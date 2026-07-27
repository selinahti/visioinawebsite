# visioina.com

The Visioina website. Plain Markdown + Jekyll, built automatically by GitHub
Pages — there is no build step to run and nothing to install.

**Every change you push to `main` is live in about a minute.** You can edit any
file directly on github.com: open it, press the pencil icon, edit, then
"Commit changes".

---

## Adding a new app

1. In `_apps/`, copy the whole `otus/` folder and rename it, e.g. to `minde/`.
   (On github.com it is easier to create the new files one at a time, using the
   OTUS files as a template.)
2. In **every file** of the new folder, change these two lines:
   - `app_slug: otus` → `app_slug: minde`
   - `permalink: /apps/otus/…` → `permalink: /apps/minde/…`
3. In `index.md`, edit the rest of the front matter: `app_name`, `tagline`,
   `summary`, `features`, `tiers`, `screenshots`.
4. Put the images in `assets/apps/minde/`.

The app then appears automatically on the home page and on `/apps/`, with its
own dark space-themed page plus privacy, terms, support and FAQ pages.

| File | What it is | Used for |
|---|---|---|
| `index.md` | The app's landing page | Link this from the App Store description |
| `privacy.md` | Privacy policy | **Privacy Policy URL** in App Store Connect |
| `support.md` | Support page | **Support URL** in App Store Connect |
| `terms.md` | Terms of use | Linked from the description |
| `faq.md` | Long FAQ | Linked from the app and the support page |

**When an app goes live**, paste the App Store link into `appstore_url:` in its
`index.md`. The "Coming soon" button turns into a real download button.

### Screenshots

Screenshots straight from the simulator are far too large for a web page
(around 2.5 MB each). Shrink them first:

```bash
sips -Z 1180 raw.png --out tmp.png && sips -s format jpeg -s formatOptions 80 tmp.png --out shot-01.jpg
```

Then list them under `screenshots:` in `index.md`, each with an `alt:`
description for screen readers.

---

## Editing texts

| What | Where |
|---|---|
| Home page | `index.html` |
| Apps overview | `apps.html` |
| Contact page | `contact.html` |
| OTUS pages | `_apps/otus/` |
| Company name, business ID, city, email | `_config.yml` → `company:` |
| Top menu links | `_data/nav.yml` |
| Colours, fonts, spacing | `assets/css/site.css` |

The company details in `_config.yml` are written into the footer of every page
and into the contact page, so changing them once changes them everywhere.

Markdown basics for the app pages: `## Heading`, `**bold**`, `*italic*`,
`[link text](https://example.com)`, and `- ` at the start of a line for a
bullet.

---

## Apple Developer Program

Apple verifies organisation Developer Program accounts by looking at this
website. Keep all of these true:

- the exact legal name **Visioina Oy** and Business ID **3352691-4** appear in
  the footer of every page
- the domain stays registered to Visioina Oy, not to a private person
- every page in the menu has real content — a placeholder or "under
  construction" page is the most common reason verification fails
- the site is reachable over HTTPS before you submit the application

---

## Connecting the domain

Once `visioina.com` is bought (register it to **Visioina Oy** — Apple checks
this):

1. At the registrar, add these DNS records:

   ```
   A     @    185.199.108.153
   A     @    185.199.109.153
   A     @    185.199.110.153
   A     @    185.199.111.153
   AAAA  @    2606:50c0:8000::153
   AAAA  @    2606:50c0:8001::153
   AAAA  @    2606:50c0:8002::153
   AAAA  @    2606:50c0:8003::153
   CNAME www  selinahti.github.io.
   ```

2. Create a file named `CNAME` in this repository containing one line:
   `visioina.com`
3. In `_config.yml`, change:
   ```yaml
   url: "https://visioina.com"
   baseurl: ""
   ```
4. On GitHub: **Settings → Pages → Custom domain** → `visioina.com` → Save, wait
   for the certificate, then tick **Enforce HTTPS**.

---

## Running the site on your own computer (optional)

Not required — GitHub builds the site for you. If you ever want a local
preview, you need Ruby (the macOS system Ruby 2.6 is too old for current
Jekyll):

```bash
bundle install && bundle exec jekyll serve --livereload
```
