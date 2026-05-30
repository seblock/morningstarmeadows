# Morning Star Meadows Website – Editing & Deployment Guide

## Overview

This website is built with:

* Hugo static site generator
* Meghna Hugo theme
* GitHub Pages deployment
* GitHub Actions for automatic deployment

Repository:

[https://github.com/seblock/morningstarmeadows](https://github.com/seblock/morningstarmeadows)

---

# How Deployment Works

When changes are pushed to the `master` branch:

1. GitHub Actions automatically runs
2. Hugo builds the website
3. Static files are generated into `/docs`
4. GitHub Pages publishes the site

Deployment workflow file:

```text
.github/workflows/main.yml
```

Important settings:

```yaml
on:
  push:
    branches:
      - master
```

```yaml
run: hugo --minify
```

```yaml
publish_dir: ./docs
```

The Hugo configuration also confirms this:

```toml
publishDir = "docs"
```

---

# First-Time Setup

## 1. Install Git

Download Git for Windows:

[https://git-scm.com/download/win](https://git-scm.com/download/win)

After installation:

```powershell
git --version
```

---

## 2. Install Hugo

This project uses Hugo version `0.91.2`.

Download the **Extended** version:

[https://github.com/gohugoio/hugo/releases/tag/v0.91.2](https://github.com/gohugoio/hugo/releases/tag/v0.91.2)

Download:

```text
hugo_extended_0.91.2_Windows-64bit.zip
```

Extract somewhere like:

```text
C:\Hugo\
```

Add that folder to your Windows PATH.

Verify installation:

```powershell
hugo version
```

Expected output:

```text
v0.91.2
```

---

## 3. Clone the Repository

```powershell
git clone https://github.com/seblock/morningstarmeadows.git
cd morningstarmeadows
```

---

# Running the Site Locally

Start the local development server:

```powershell
hugo server
```

Open:

```text
http://localhost:1313
```

The site automatically refreshes when files are edited.

---

# Where to Edit Content

## Main Site Content

Most editable content is located in:

```text
content/english/
```

Examples:

| Section  | Location                    |
| -------- | --------------------------- |
| About    | `content/english/about/`    |
| Products | `content/english/products/` |
| Contact  | `content/english/contact/`  |

---

## Images

General images:

```text
static/images/
```

Site-specific images:

```text
static/images/siteSpecific/
```

---

## Navigation Menu

Edit:

```text
config.toml
```

Menu items are configured under:

```toml
[[Languages.en.menu.main]]
```

Example:

```toml
[[Languages.en.menu.main]]
name = "Products"
url = "/products"
weight = 3
```

---

## Social Media Links

Also in:

```text
config.toml
```

Section:

```toml
[[params.social]]
```

Example:

```toml
link = "https://www.facebook.com/..."
```

---

## Site Title and SEO

Edit in:

```text
config.toml
```

Example:

```toml
title = "Morning Star Meadows Family Farm"
description = "..."
```

---

# Redeploying the Site

## 1. Save Your Changes

Edit content, images, or configuration files.

---

## 2. Test Locally

```powershell
hugo server
```

Verify the site looks correct.

---

## 3. Commit Changes

```powershell
git add .
git commit -m "Updated website content"
```

---

## 4. Push Changes

```powershell
git push origin master
```

---

# Automatic Deployment

After pushing:

1. GitHub Actions automatically rebuilds the site
2. GitHub Pages redeploys the updated version

Deployment usually completes within 1–3 minutes.

You can monitor deployment status in:

```text
GitHub Repository → Actions tab
```

---

# Important Notes

## Do Not Delete `/docs`

The `/docs` folder contains the generated production website.

GitHub Pages publishes directly from this folder.

---

## Manual Build Command

If needed, manually rebuild the production files:

```powershell
hugo --minify
```

This regenerates the `/docs` directory.

---

# Recommended Workflow

Each time you want to make updates:

```powershell
git pull
hugo server
```

Make edits.

Then deploy:

```powershell
git add .
git commit -m "Describe changes"
git push
```

Done.

---

# Optional Visual CMS Tools

This project previously used Forestry CMS, which has been discontinued.

Possible replacements:

* Decap CMS — [https://decapcms.org/](https://decapcms.org/)
* CloudCannon — [https://cloudcannon.com/](https://cloudcannon.com/)
* TinaCMS — [https://tina.io/](https://tina.io/)

These tools provide visual editing instead of manually editing markdown files.
