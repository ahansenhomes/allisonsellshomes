# Allison Sells Homes — Deployment Guide

This is the complete website for allisonsellshomes.com, ready to deploy to Netlify with Decap CMS for content editing.

---

## Folder structure

```
allisonsellshomes/
├── index.html           ← your website
├── netlify.toml         ← Netlify configuration
├── README.md            ← this file
├── _data/
│   ├── settings.json    ← phone, email, address, stats, hero text
│   ├── reviews.json     ← client reviews
│   ├── blog.json        ← blog post previews
│   ├── faq_buyers.json  ← buyer FAQ questions & answers
│   ├── faq_sellers.json ← seller FAQ questions & answers
│   └── faq_espanol.json ← Spanish FAQ questions & answers
├── admin/
│   ├── index.html       ← Decap CMS editor UI
│   └── config.yml       ← tells Decap what content is editable
└── images/              ← add your photos here (create this folder)
```

---

## Step 1 — Create a GitHub account and repository

1. Go to **github.com** and sign up for a free account if you don't have one
2. Click the **+** icon (top right) → **New repository**
3. Name it `allisonsellshomes` (or anything you like)
4. Set it to **Public**
5. Click **Create repository**

---

## Step 2 — Upload your files to GitHub

**Option A — drag and drop (easiest):**
1. Open your repository on GitHub
2. Click **uploading an existing file** (shown on the empty repo page)
3. Drag the entire `allisonsellshomes` folder contents into the upload area
4. Make sure the folder structure is preserved (all files and subfolders)
5. Scroll down, click **Commit changes**

**Option B — GitHub Desktop app:**
1. Download GitHub Desktop from desktop.github.com
2. Clone your new repository to your computer
3. Copy all the files into the cloned folder
4. In GitHub Desktop, click **Commit to main** → **Push origin**

---

## Step 3 — Deploy to Netlify

1. Go to **netlify.com** and sign up for a free account
2. Click **Add new site** → **Import an existing project**
3. Choose **GitHub** and authorize Netlify to access your account
4. Select your `allisonsellshomes` repository
5. Leave all build settings blank (this is a plain HTML site, no build needed)
6. Click **Deploy site**

Your site will be live at a temporary URL like `random-name-123.netlify.app` within about 30 seconds.

---

## Step 4 — Connect your custom domain

1. In Netlify, go to **Site configuration** → **Domain management**
2. Click **Add a domain** and type `allisonsellshomes.com`
3. Netlify will show you DNS settings — either:
   - **Nameservers** (if you want Netlify to manage DNS fully), or
   - **A record / CNAME** (if you want to keep your domain registrar managing DNS)
4. Log into wherever your domain is registered (GoDaddy, Namecheap, Squarespace, etc.)
5. Update the DNS settings as instructed by Netlify
6. Wait 1–48 hours for DNS to propagate (usually under 2 hours)
7. Netlify automatically provisions a free SSL certificate (https) once DNS is active

---

## Step 5 — Set up Netlify Identity (for CMS login)

1. In Netlify, go to **Site configuration** → **Identity**
2. Click **Enable Identity**
3. Under **Registration**, set to **Invite only** (so only you can log in)
4. Scroll down to **Services** → **Git Gateway** → click **Enable Git Gateway**
   - This is what allows the CMS to save edits back to GitHub
5. Go to **Identity** → **Invite users** → enter your email address
6. Check your email and accept the invitation — this creates your CMS login

---

## Step 6 — Update the CMS config with your GitHub username

Before this step, open `admin/config.yml` and replace `YOUR_GITHUB_USERNAME` on line 2 with your actual GitHub username:

```yaml
backend:
  name: github
  repo: YOUR_GITHUB_USERNAME/allisonsellshomes   ← change this
  branch: main
```

Commit and push that change to GitHub, and Netlify will redeploy automatically.

---

## Step 7 — Log into your CMS

1. Go to `https://allisonsellshomes.com/admin`
2. Log in with the email and password you set in Step 5
3. You'll see the Decap CMS dashboard with these editable sections:
   - **Site Settings** — phone, email, address, stats, hero text
   - **Reviews** — add, edit, or remove client reviews
   - **Blog Posts** — add new posts or update existing ones
   - **Buyer FAQ** — edit questions and answers
   - **Seller FAQ** — edit questions and answers
   - **FAQ en Español** — edit Spanish FAQ questions and answers
4. Make a change, click **Save**, then **Publish** — the site updates within ~30 seconds

---

## Adding your photo

The site has a photo placeholder in the hero and about sections. To add your headshot:

1. Create an `images` folder inside your site files
2. Add your photo as `images/allison.jpg` (3:4 portrait format works best)
3. In `index.html`, find the two `hero-photo-box` divs and replace the SVG placeholder with:
   ```html
   <img src="/images/allison.jpg" alt="Allison Hansen" style="width:100%; border-radius: 8px;">
   ```

---

## Making text edits beyond what the CMS covers

The CMS handles reviews, blog posts, FAQs, and key stats. For other text changes (like page headings, the about section bio, neighborhood descriptions), you can:

1. Open `index.html` directly on GitHub
2. Click the pencil icon (Edit)
3. Make your change
4. Click **Commit changes** — Netlify redeploys automatically within 30 seconds

---

## Need help?

If anything isn't working, the most common issues are:

- **CMS won't save** — make sure Git Gateway is enabled (Step 5) and your GitHub username is correct in `config.yml` (Step 6)
- **Site not showing after domain change** — DNS propagation can take up to 48 hours; check back later
- **Reviews/blog not loading** — make sure the `_data` folder uploaded correctly to GitHub with all 5 JSON files inside
