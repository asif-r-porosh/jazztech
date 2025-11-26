# JazzTech Website – Installation, Editing, and Deployment Guide

This document provides clear instructions for editing, updating, and deploying the JazzTech static website using GitHub Pages, along with **GoDaddy domain configuration**.

---

## 1. Overview

The JazzTech website is a **static one‑page site** built with HTML, CSS, and Bootstrap.  
No frameworks, no backend, no build pipeline — simple, fast, and reliable.

It is deployed through **GitHub Pages** and uses a **GoDaddy-purchased domain**.

---

## 2. Project Structure

```
.
├── index.html
├── assets/
│   ├── css/
│   ├── js/
│   └── favicon/
│       ├── android-chrome-192x192.png
│       ├── android-chrome-512x512.png
│       ├── apple-touch-icon.png
│       ├── favicon-16x16.png
│       ├── favicon-32x32.png
│       ├── favicon.ico
│       └── site.webmanifest
└── .nojekyll
```

---

## 3. Editing the Website

### Edit HTML

Open `index.html` and modify:

- Text content
- Sections
- Navbar items
- Layout
- Contact information

Any standard text editor works (VS Code recommended).

### Edit Styles

Custom styles may exist under:

```
assets/css/
```

You can add more CSS in a new file:

```
assets/css/custom.css
```

Then include it in `index.html`.

---

## 4. Running Locally

#### Option A — Double-click

Just open:

```
index.html
```

Or drag-drop it into your browser.

#### Option B — Local HTTP server (recommended)

```
python3 -m http.server
```

Visit:

```
http://localhost:8000
```

---

## 5. Updating the Live Site

GitHub Pages automatically deploys whenever you push to the `main` branch.

### Commit and push changes:

```bash
git add .
git commit -m "Update website content"
git push origin main
```

Within ~30 seconds, GitHub Pages will update.

---

## 6. Replacing the Entire Site (Safe Method)

1. Backup old site:

```bash
git checkout main
git pull
git branch old-site
git push -u origin old-site
```

2. Replace the files in `main` with your new files:

```bash
git rm -r .
# Copy new site files into the repo
git add .
git commit -m "Replace website with new version"
git push origin main
```

`old-site` contains the previous site if needed.

---

## 7. Deploying via GitHub Pages

### 1. Open GitHub → Repository Settings → Pages  
### 2. Configure:

- **Source:** `main` branch  
- **Folder:** `/ (root)`  
- Save.

### 3. Ensure `.nojekyll` exists (required for raw static files):

If missing:

```bash
touch .nojekyll
git add .nojekyll
git commit -m "Add .nojekyll for GitHub Pages"
git push origin main
```

Your site will be published at:

```
https://<your-username>.github.io/<repo-name>/
```

---

## 8. Connecting GoDaddy Domain to GitHub Pages

### Step 1 — In GitHub Pages Settings

Go to:

**Settings → Pages → Custom Domain**

Enter your domain:

```
yourdomain.com
```

Click **Save**.

GitHub will give you **two A records** and **one CNAME**.

Typically:

```
A     @      185.199.108.153
A     @      185.199.109.153
A     @      185.199.110.153
A     @      185.199.111.153
CNAME www    <your-username>.github.io
```

### Step 2 — Go to GoDaddy DNS settings

1. Login to GoDaddy  
2. Go to **My Products**  
3. Choose your domain  
4. Click **DNS**  
5. Remove existing A records  
6. Add the GitHub A records  
7. Add the GitHub CNAME

### Step 3 — Wait for propagation

DNS updates take **5 minutes to 1 hour**.

### Step 4 — Enable HTTPS

Back in GitHub Pages, enable:

```
✔ Enforce HTTPS
```

---

## 9. Verification

Test:

```
https://yourdomain.com
https://www.yourdomain.com
```

Both should work and redirect properly.

---

## 10. Troubleshooting

### If site doesn't update:
- Clear browser cache  
- Wait 1–5 minutes  
- Check GitHub Actions (Pages build logs)  
- Ensure `.nojekyll` exists  

### If domain doesn’t resolve:
- Recheck GoDaddy A records  
- Remove conflicting records  
- Ensure CNAME is correct  

---

## 11. License

Content belongs to JazzTech.  
Do not reuse branding or text without permission.

---

End of guide.
