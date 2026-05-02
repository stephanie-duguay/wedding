# Stephanie & Jeffrey — Wedding Website

A private, password-protected wedding website built as a single HTML file. Deployable for free on GitHub Pages.

---

## What's in this folder

- **`index.html`** — The entire site (HTML, CSS, JavaScript, and embedded photos all in one file).
- **`README.md`** — This file.

That's it. There's no build step, no dependencies, no framework to install.

---

## Deploying to GitHub Pages

### Step 1 — Create a GitHub account
If you don't already have one, sign up at [github.com](https://github.com). It's free.

### Step 2 — Create a new repository
1. Click the **+** icon (top right) → **New repository**.
2. Name it something like `wedding-site` or `stephanie-and-jeffrey`.
3. Choose **Public** (required for free GitHub Pages — but don't worry, your site is still password-protected).
4. Check **Add a README file**.
5. Click **Create repository**.

### Step 3 — Upload `index.html`
1. On your new repo's main page, click **Add file** → **Upload files**.
2. Drag `index.html` into the upload area.
3. Scroll down and click **Commit changes**.

### Step 4 — Enable GitHub Pages
1. In your repo, click **Settings** (top right of the repo nav).
2. In the left sidebar, click **Pages**.
3. Under **Source**, select **Deploy from a branch**.
4. Under **Branch**, select **main** and **/ (root)**, then click **Save**.
5. Wait 1–2 minutes. GitHub will give you a URL like:
   `https://<your-username>.github.io/<repo-name>/`

That's your live wedding site. Share that link with guests along with the password.

---

## Editing the site after launch

All of the content guests see — the password, hero text, event details, guest list, FAQs, registry message — is stored in a single `CONFIG` object near the top of `index.html`. Look for the comment block that says:

```
// ╔══════════════════════════════════════════════════════════════════════════════╗
// ║   ✏️  EDIT EVERYTHING IN THE CONFIG BELOW  ✏️                                ║
// ╚══════════════════════════════════════════════════════════════════════════════╝
```

Anything below the matching **STOP** comment block is the rendering engine — you shouldn't need to touch it.

### To update content:
1. Open `index.html` in any text editor (VS Code, Notepad, Sublime, etc.).
2. Edit the values inside the `CONFIG` object.
3. Save the file.
4. In your GitHub repo, click `index.html` → the pencil icon (edit) → paste your updated file (or upload-replace).
5. Commit changes. The site updates within ~1 minute.

### Common edits

| What you want to change | Where to look |
|---|---|
| Site password | `sitePassword` |
| Names on hero / homepage | `partner1FirstName`, `partner2FirstName` |
| Wedding date or venue | `events[]` and `venue` |
| Day-of timeline | `timeline[]` |
| Guest list | `parties[]` |
| FAQs | `faqs[]` |
| Hero photo | `heroImageUrl` |

---

## RSVP responses

By default, RSVPs save to **localStorage in each guest's browser** — fine for testing, but you'll want them collected in one place.

### To collect RSVPs in a Google Sheet:
1. Create a new Google Sheet.
2. In the Sheet, go to **Extensions → Apps Script**.
3. Paste a Google Apps Script that accepts POST requests and writes to the Sheet (search "Google Apps Script wedding RSVP" for templates, or ask Claude to generate one for you).
4. Deploy the script as a **Web app** with access set to **Anyone**.
5. Copy the deployment URL.
6. In `index.html`, find `googleSheetsUrl: ""` in the CONFIG and paste your URL between the quotes.

### To view RSVPs (admin):
On the live site, scroll to the very bottom and click the small **•** dot in the footer. Enter your `adminPassword` (set in CONFIG) to view and export all responses.

---

## Custom domain (optional)

If you want a friendlier URL like `stephandjeff.com` instead of `username.github.io/wedding-site`:

1. Buy a domain (Namecheap, Google Domains, Cloudflare Registrar, etc.).
2. In your repo's **Settings → Pages**, enter your domain under **Custom domain**.
3. In your domain registrar's DNS settings, add a CNAME record pointing to `<your-username>.github.io`.
4. Wait for DNS to propagate (a few minutes to a few hours).

GitHub will automatically issue an HTTPS certificate.

---

## Troubleshooting

**The page is blank or shows raw code.**
Make sure the file is named exactly `index.html` (lowercase) and is at the root of the repo, not inside a subfolder.

**Changes I made aren't showing up.**
GitHub Pages caches aggressively. Hard-refresh your browser (Ctrl+Shift+R on Windows, Cmd+Shift+R on Mac) or open in an incognito window.

**The password doesn't work.**
Check that the password in CONFIG matches what you're typing exactly — passwords are case-sensitive.

**RSVPs aren't appearing in my Google Sheet.**
Confirm the Apps Script is deployed as **Anyone can access** and that the URL in CONFIG is the `/exec` URL, not the `/dev` URL.

---

## Notes

- Photos in this template are embedded as base64 directly in the HTML, which keeps everything in one file but makes the file large (~650KB). If you swap them for hosted image URLs (e.g., uploaded to Imgur, Cloudinary, or your own image host), the file shrinks dramatically and loads faster.
- The site works offline once loaded, since it's a single file with no external dependencies beyond Google Fonts.
- Password protection is client-side only — anyone who views the page source can find the password. This is fine for keeping casual visitors out, but don't put truly sensitive info on the page.
