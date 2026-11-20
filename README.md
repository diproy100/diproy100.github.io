# Dipayan Roy: Personal Site & Tech Blog

Source for **https://diproy100.github.io**, built with [Hugo](https://gohugo.io) and the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme, and hosted free on GitHub Pages.

---

## One-time setup (about 20 minutes)

### 1. Create the repository
1. Sign in to GitHub as **diproy100**.
2. Click **+ → New repository**.
3. Name it exactly **`diproy100.github.io`**, set it to **Public**, and leave every "initialize" box unticked.
4. Click **Create repository**.

### 2. Upload the files
1. On the new empty repo page, click **"uploading an existing file"**.
2. Unzip `diproy100-site.zip` on your computer, open the unzipped folder, select **everything inside it**, and drag it into the browser.
3. Click **Commit changes**.

> ⚠️ **Check the `.github` folder uploaded.** Folders that start with a dot are sometimes hidden or skipped.
> After uploading, check that the repo contains `.github/workflows/hugo.yml`. If it's missing:
> **Add file → Create new file**, type the name `.github/workflows/hugo.yml`, paste in that file's contents, and commit.

### 3. Turn on GitHub Pages
1. Go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **GitHub Actions**.
3. Open the **Actions** tab. A "Deploy site to GitHub Pages" run should start, or start it with **Run workflow**.
4. When it shows a green tick (about a minute), your site is live at **https://diproy100.github.io** 🎉

### 4. Turn on comments (Giscus)
1. In the repo, go to **Settings → General → Features** and tick **Discussions**.
2. Install the Giscus app at https://github.com/apps/giscus and give it access to `diproy100.github.io` only.
3. Go to https://giscus.app, enter the repo `diproy100/diproy100.github.io`, and choose the **Announcements** discussion category.
4. In the generated script near the bottom of that page, copy the values of `data-repo-id` and `data-category-id`.
5. Paste them into `hugo.yaml` under `params → giscus → repoId` and `categoryId`, then commit.

You moderate comments (delete, lock, etc.) from the repo's **Discussions** tab.

### 5. Turn on visitor analytics (GoatCounter)
1. Sign up free at https://www.goatcounter.com/signup and pick the code **`diproy100`** (or any code you like).
2. In `hugo.yaml`, set `goatcounter: "diproy100"` (your code only, not the full URL) and commit.
3. See your stats at `https://diproy100.goatcounter.com`.

---

## Writing a blog post

1. In the repo, open `content/posts/` and click **Add file → Create new file**.
2. Name it with lowercase words and hyphens, for example `onestream-business-rule-tips.md`. The name becomes the post's web address.
3. Paste this header, then write your post in Markdown below it:

```yaml
---
title: "OneStream Business Rule Tips"
date: 2026-11-25
draft: false
tags: ["OneStream", "Business Rules"]
summary: "One or two sentences shown in the post list and search."
comments: true      # false = no comments on this post
ShowToc: true       # table of contents for long posts
---
```

4. Click **Commit changes**. The site rebuilds and the post appears about a minute later.

**Tips**
- `draft: true` keeps a post hidden until you're ready.
- A date in the future also keeps a post hidden until that date (after the next rebuild).
- Put images in `static/images/` and use them in a post with `![Alt text](/images/my-picture.png)`.
- Code blocks get syntax highlighting: start them with three backticks plus a language, for example ```` ```vbnet ````, ```` ```python ```` or ```` ```sql ````.
- **Turning comments on or off:** change `comments: true` / `comments: false` in a post's header.

## Editing other pages

| What | File |
|---|---|
| Home page headline, photo, buttons, social links, menu | `hugo.yaml` |
| About page | `content/about.md` |
| Experience page | `content/experience.md` |
| Contact page | `content/contact.md` |
| Profile photo | `static/images/profile.jpg` (replace with a square image, same name) |

## Previewing on your own computer (optional)

Install Hugo (extended), then run:

```bash
git clone https://github.com/diproy100/diproy100.github.io
cd diproy100.github.io
git clone --depth 1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
hugo server
```

Then open http://localhost:1313.

## Using a custom domain later

Buy a domain, then add it under **Settings → Pages → Custom domain**, and update `baseURL` in `hugo.yaml`. Nothing else needs to change.
