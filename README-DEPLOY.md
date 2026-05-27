# Deploying the Year 9 Computing site to GitHub Pages

Public repo: **`year9-computing`** → live URL: **`https://yunshugao.github.io/year9-computing/`**

You'll do this once. After that, redeploying is **three commands**.

## One-time setup (10 minutes)

### 1. Create a NEW public repo on GitHub
Open <https://github.com/new> and fill in:
- **Owner:** YunshuGao
- **Repository name:** `year9-computing`
- **Description:** `Year 9 Computing - interactive worksheets (9 COTYB & 9 COTYC)`
- **Public** (must be public for free GitHub Pages)
- ❌ Do **NOT** tick "Add a README file" / `.gitignore` / license — this folder already has files.

Click **Create repository**.

### 2. Push this folder to that repo
Open a terminal in this folder (`Web-Deploy/`) and run:

```bash
cd "D:/NEW_YunshuGao_2026_Teaching/9 COTYC-2026_GTPA/Web-Deploy"
git init
git add .
git commit -m "Initial Year 9 Computing worksheets"
git branch -M main
git remote add origin https://github.com/YunshuGao/year9-computing.git
git push -u origin main
```

### 3. Enable GitHub Pages
On the new repo page:
1. Click **Settings** (top right of the repo).
2. Left sidebar: click **Pages**.
3. Under **Source**, choose **Deploy from a branch**.
4. Branch: **main**, folder: **/ (root)**. Click **Save**.
5. Wait 1–2 minutes. Refresh the Pages settings page — it will say
   _"Your site is live at https://yunshugao.github.io/year9-computing/"_.

### 4. Test the URL
Open <https://yunshugao.github.io/year9-computing/> in any browser. You should see the Year 9 Computing landing page with three lesson cards. **Write this URL on the whiteboard tomorrow.**

---

## Tomorrow's lesson — what to tell students

> Open your browser. Go to **yunshugao.github.io/year9-computing** *(write on board)*.
> Click the green **Lesson 1** card. Use the **numbered tabs at the top** to move between Sections 1 to 7 of the worksheet. When you finish, click **Save my work as .html** to hand in.

---

## Re-deploying after a content change

Anytime you edit content (e.g., update `CURRENT_LESSON` in `build_interactive_guides.py` before the next class), regenerate and push:

```bash
# Regenerates BOTH Teaching Resources/ and Web-Deploy/
python "D:/NEW_YunshuGao_2026_Teaching/9 COTYC-2026_GTPA/_build/build_interactive_guides.py"

# Then in Web-Deploy/, push the update
cd "D:/NEW_YunshuGao_2026_Teaching/9 COTYC-2026_GTPA/Web-Deploy"
git add .
git commit -m "Update content"
git push
```

The site updates ~30 seconds after the push.

---

## Rolling the "TODAY" badge between lessons

Open `_build/build_interactive_guides.py`. Near the top, find:

```python
CURRENT_LESSON = 1
```

Change `1` → `2` after tomorrow, then `2` → `3` after the next lesson. Regenerate and push (commands above).

---

## What's in this folder

| File | Purpose |
|---|---|
| `index.html` | Landing page — "Year 9 Computing" header with 3 lesson cards |
| `g8.html` | Lesson 1 — HTML Guide 8: Menus, Forms and Images (with embedded basketball image) |
| `js1.html` | Lesson 2 — JS Guide 1: Meet JavaScript |
| `js2.html` | Lesson 3 — JS Guide 2: Buttons and Functions |
| `README-DEPLOY.md` | This file. Keep in the repo as documentation. |

Each `.html` is a single self-contained file (CSS + JS + embedded image all inline). No build step, no dependencies, no internet needed AT student-side after page loads.

---

## What students see (navigation)

Inside each worksheet:
1. **Header bar** with their name, date, and a "Save my work as .html" button.
2. **Numbered tabs (1 through 7)** at the top — one click jumps to that section.
3. **One section at a time** — less overwhelming than scrolling 21 task panels.
4. **Prev / Next buttons** at the bottom of each section.
5. **Position indicator** ("Section 3 of 7").
6. **← / → arrow keys** also navigate (when not typing in the editor).

Their work auto-saves in browser localStorage, **per worksheet** (so JS Guide 1 doesn't clobber HTML Guide 8). They click **Save my work as .html** at the end to download their submission file.

---

## Growth: adding more units later

The repo name `year9-computing` is generic on purpose. To add a second unit (e.g., a Term 3 unit), drop more `.html` files into the repo, edit `index.html` to add cards for them, and push. The site grows; the URL stays the same.

If you want to add a different class (e.g., Year 10) under the same site, create a subfolder like `/year10/` inside the repo and link to it from `index.html`. Same URL pattern: `yunshugao.github.io/year9-computing/year10/...`. Or — cleaner — make a new repo `year10-computing` and link between them.

---

## Troubleshooting

**"It's been 5 minutes and the URL still says 404."**
Pages can take up to 10 min on first deploy. Check **Settings → Pages** — it shows the deployment status.

**School WiFi blocks github.io.**
Test it yourself on the school network first. If blocked, ask IT to whitelist `*.github.io`. Backup: use Netlify Drop (drag the Web-Deploy folder onto <https://app.netlify.com/drop>) — gives you an instant `*.netlify.app` URL.

**A student's work disappeared.**
Their work auto-saves in their browser's `localStorage` for that exact URL. If they clear cookies/cache, or use a different browser, or a different machine, the saved work won't be there. Tell them to click **Save my work as .html** before closing the tab.

**I want to change which lesson is "today".**
See the "Rolling the TODAY badge" section above.

**The page is private — I want only my class to see it.**
GitHub Pages free tier serves all public repos. To keep it private you'd need GitHub Pro or a different host (e.g., a password-protected Netlify site). For most NSW classroom use this isn't needed; the URL is obscure and the content is teaching material.
