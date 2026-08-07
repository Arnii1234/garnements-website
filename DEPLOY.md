# garnements — deploying

## First: look at it locally

The curved page flip uses WebGL, and browsers refuse to load images into WebGL
when a page is opened as a file (double-clicking `index.html`). Opened that way
the site still works — it just falls back to the flat flip. To see the real
thing you need to serve the folder.

Open Terminal and run:

    cd ~/Desktop/"garnements website"
    python3 -m http.server 8000

Then go to <http://localhost:8000> in your browser. Press `Ctrl-C` in Terminal
to stop it when you're done.

If the flip looks flat rather than curved, open the browser console
(`Cmd-Option-J` in Chrome) and check for errors — that tells us whether three.js
failed to load or WebGL is unavailable.

## Put it on GitHub Pages

You need a GitHub account. Everything below is copy-paste.

### 1. Make the repository

On <https://github.com/new>:

- **Repository name:** `garnements`
- **Public**
- Do **not** tick "Add a README" — the folder already has files

Leave the page open, you'll need the URL it shows you.

### 2. Push the folder

In Terminal:

    cd ~/Desktop/"garnements website"
    git init
    git add .
    git commit -m "garnements 2026"
    git branch -M main
    git remote add origin https://github.com/YOUR-USERNAME/garnements.git
    git push -u origin main

Replace `YOUR-USERNAME` with your GitHub username. Git will ask you to sign in;
use the browser option if offered.

### 3. Turn Pages on

In the repository: **Settings → Pages**.

- **Source:** Deploy from a branch
- **Branch:** `main`, folder `/ (root)`
- **Save**

Give it a minute or two, then your site is at:

    https://YOUR-USERNAME.github.io/garnements/

That URL is served over https, so WebGL will work.

### Updating it later

After any change:

    cd ~/Desktop/"garnements website"
    git add .
    git commit -m "what changed"
    git push

The live site updates within a minute.

## Adding garnements.de later

Nothing about the site changes — it's two steps.

**At your registrar**, add these DNS records for the bare domain:

| Type | Name | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `YOUR-USERNAME.github.io` |

**In the repository**, Settings → Pages → Custom domain: enter `garnements.de`,
save, and tick "Enforce HTTPS" once it becomes available (can take a few hours
while the certificate is issued).

Registrars worth using for `.de`: INWX (Berlin, ~€5/yr), Netcup (~€5/yr),
Spaceship (~€3.50/yr). Check the *renewal* price, not the first-year offer.

## What's in the folder

    index.html        the whole site — markup, styles and script in one file
    assets/           artwork: title, 10 page drawings, 10 garment drawings
    .nojekyll         tells GitHub Pages to serve the files as-is
    DEPLOY.md         this file

## Things still to do

- Checkout sends an email; there's no online payment yet (intentionally deferred — revisit if/when you want Stripe or similar)
