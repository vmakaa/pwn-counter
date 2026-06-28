# CTF Writeups

A static site for CTF challenge writeups, built with [Jekyll](https://jekyllrb.com/) and the [just-the-docs](https://just-the-docs.com/) theme, deployed via GitHub Pages.

## 🚀 One-time setup (do this first)

1. **Create a new repo on GitHub** named `ctf-writeups` (or whatever you like — just update `baseurl` in `_config.yml` to match).
2. **Push this folder to it:**
   ```bash
   cd ctf-writeups
   git init
   git add .
   git commit -m "Initial site setup"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/ctf-writeups.git
   git push -u origin main
   ```
3. **Edit `_config.yml`:**
   - Replace `YOUR-USERNAME` in `url` and the `aux_links` GitHub link with your actual GitHub username.
   - If your repo is named something other than `ctf-writeups`, update `baseurl` to match (e.g. `/my-repo-name`). If you're using a custom domain, set `baseurl: ""`.
4. **Enable GitHub Pages with Actions:**
   - Go to your repo → **Settings → Pages**.
   - Under "Build and deployment", set **Source** to **GitHub Actions**.
   - That's it — the included workflow (`.github/workflows/pages.yml`) will build and deploy automatically on every push to `main`.
5. **Wait ~1-2 minutes**, then check the **Actions** tab to watch it build. Your site will be live at:
   ```
   https://YOUR-USERNAME.github.io/ctf-writeups/
   ```

## ✍️ Adding a new writeup

1. Copy `_TEMPLATE.md` into the right category folder (`web/`, `pwn/`, `crypto/`, `reverse-engineering/`, `forensics/`, or `misc/`).
2. Rename it something descriptive, e.g. `web/htb-flask-ssti.md`.
3. Fill in the front matter at the top:
   ```yaml
   ---
   title: "HTB: Flask SSTI"
   parent: Web Exploitation
   nav_order: 2
   ---
   ```
   - `parent` must exactly match the `title` of one of the category index pages (see table below).
   - `nav_order` controls position in the sidebar within that category (lower = higher up).
4. Write the content below the front matter using normal Markdown.
5. Commit and push — the site rebuilds automatically.

| Folder | `parent` value to use |
|---|---|
| `web/` | `Web Exploitation` |
| `pwn/` | `Pwn / Binary Exploitation` |
| `crypto/` | `Cryptography` |
| `reverse-engineering/` | `Reverse Engineering` |
| `forensics/` | `Forensics` |
| `misc/` | `Misc` |

## 🖥️ Running locally (optional, to preview before pushing)

You'll need Ruby installed.

```bash
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000/ctf-writeups/` in your browser. Changes to files will auto-rebuild while `jekyll serve` is running.

## 🗂️ Project structure

```
ctf-writeups/
├── _config.yml          # site config (title, theme, baseurl, etc.)
├── index.md              # homepage
├── _TEMPLATE.md          # copy this for every new writeup
├── web/                   # Web Exploitation writeups
│   └── index.md           # category landing page (do not delete)
├── pwn/                   # Pwn / Binary Exploitation writeups
├── crypto/                # Cryptography writeups
├── reverse-engineering/   # Reverse Engineering writeups
├── forensics/             # Forensics writeups
├── misc/                  # Misc writeups
└── .github/workflows/     # auto-deploy workflow, don't need to touch this
```

## 🎨 Customizing

- **Color scheme**: change `color_scheme` in `_config.yml` (`light`, `dark`, or define your own — see [just-the-docs docs](https://just-the-docs.com/docs/customization/)).
- **Site title/description**: edit `title` and `description` at the top of `_config.yml`.
- **Adding a category**: create a new folder, add an `index.md` inside it (copy an existing category's `index.md` as a starting point, give it a new `title` and `permalink`), then use that `title` as the `parent` for writeups in that folder.
