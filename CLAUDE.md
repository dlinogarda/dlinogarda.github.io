# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Static personal academic portfolio website for Lino Garda Denaro, Ph.D., hosted on GitHub Pages at `dlinogarda.com` (CNAME). There is no build system, bundler, or package manager — everything ships as-is.

## Previewing locally

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Or any static file server will work. Opening `index.html` directly in a browser also works for most things, but some assets may not load correctly without a server.

## CV (LaTeX)

The CV source is `assets/cv/main.tex`. After editing, compile and copy the output:

```bash
cd assets/cv
pdflatex main.tex
bibtex main      # if bibliography changed
pdflatex main.tex
pdflatex main.tex
cp main.pdf ../img/cv.pdf
```

`assets/img/cv.pdf` is the file the site links to for download.

## Architecture

**Single-page site** — all content lives in `index.html`. Sections are `#hero`, `#about`, `#skills`, `#resume`, `#research`, `#AwardAchievement`, `#contact`. Navigation scroll-spies against these IDs.

**Styling** — `assets/css/style.css` is the only file to edit for appearance. `styleBackup.css` is a backup of the original template style. The template is iPortfolio v3.7.0 (BootstrapMade).

**JS** — `assets/js/main.js` handles scroll-spy, typed.js animation, AOS scroll animations, mobile nav toggle, and back-to-top button. All vendor libraries are bundled locally under `assets/vendor/` — no CDN dependency for JS (except Academicons CSS which loads from both local and jsDelivr CDN).

**Publications** — listed as a numbered `<ol class="journal">` with a CSS counter that auto-prepends `[J1]`, `[J2]`, etc. Add new entries at the bottom of the list to maintain chronological numbering.

**Contact form** — `forms/contact.php` is a PHP mailer script. The form itself is inside `index.html` but GitHub Pages only serves static files, so the PHP handler must run on a separate server if contact form submission is needed.

**Dashboard Pro** — the nav links to `https://pro.dlinogarda.com/`, which is a separate project/subdomain and not part of this repo.

## Deployment

Push to `main` — GitHub Pages serves the repo root directly. No CI, no build step.
