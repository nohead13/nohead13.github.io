# Maksim Aan Landing Page

A lightweight, responsive link-in-bio website for photographer and content
creator Maksim Aan. The page directs visitors to the photo gallery, event photo
ordering, donation page, and social profiles.

The site is built entirely with HTML, CSS, and vanilla JavaScript. It has no
build process, package manager, backend, or database and can be hosted directly
with GitHub Pages.

## Current features

- Responsive, mobile-first single-page layout
- Profile image, name, role, and short introduction
- Social links for Instagram, Telegram, Facebook, YouTube, and TikTok
- Action cards for:
  - Shop & Gallery
  - Ordering Event Photography by email
  - PayPal support
- Automatic copyright year
- Keyboard-visible interactive links and accessible labels
- Reduced-motion support through `prefers-reduced-motion`
- SEO description and keyword metadata
- Open Graph and Twitter Card metadata
- SVG favicon
- Google Fonts integration using Inter

The current implementation uses a light monochrome visual style. Although the
original project brief describes a dark theme and four action buttons, the code
in this directory is the source of truth for the deployed page.

## Project structure

```text
lending-page/
├── .gitignore
├── index.html
├── style.css
├── script.js
├── PROJECT_LENDING_PAGE_DOCUMENTATION.md
├── assets/
│   ├── favicon.svg
│   └── profile.svg
└── content/
    └── profile_image.jpg
```

## Run locally on macOS

No installation is required. From the repository root, start a local static
server:

```bash
cd lending-page
python3 -m http.server 8000
```

Open [http://localhost:8000](http://localhost:8000) in a browser. Stop the
server with `Control-C`.

Opening `index.html` directly also works for basic review, but a local HTTP
server more closely matches GitHub Pages hosting.

## Customize the page

Most content is configured directly in `index.html`.

### Profile and text

Update these elements:

- Page title and SEO metadata inside `<head>`
- Profile image alternative text
- Role in `.eyebrow`
- Name in `<h1>`
- Introduction in `.tagline`
- Footer name and message

Replace `content/profile_image.jpg` to change the portrait. Keeping the same
filename requires no HTML change. The current CSS displays it as a square,
circular crop using `object-fit: cover`.

### Main links

Edit the `href` values on the three `.action-card` elements in `index.html`:

| Card | Current destination |
| --- | --- |
| Shop & Gallery | `https://maksimaan.pixieset.com` |
| Ordering Event Photography | `mailto:orderfrommaksim@gmail.com` |
| Support My Work | PayPal payment page |

To add another action, duplicate one complete `.action-card` link and update
its icon, heading, description, and URL.

### Social links

The social buttons are in `.hero-actions`. Each link contains an inline SVG and
an accessible `aria-label`. When changing a platform, update all of the
following:

- `href`
- `aria-label`
- `title`
- SVG icon path

External links use `target="_blank"` with `rel="noopener noreferrer"`.

### Colors and layout

Global design values are declared as CSS custom properties at the top of
`style.css`:

```css
:root {
  --bg: #f5f5f3;
  --panel: #ffffff;
  --text: #111111;
  --muted: #4f4f4f;
  --border: rgba(17, 17, 17, 0.12);
}
```

The primary content width is controlled by `.page-shell`. Mobile adjustments
are located in the `@media (max-width: 820px)` block.

## JavaScript behavior

`script.js` sets the current year in the footer after the DOM is ready:

```js
document.addEventListener("DOMContentLoaded", () => {
  const yearNode = document.getElementById("year");
  if (yearNode) {
    yearNode.textContent = new Date().getFullYear();
  }
});
```

The page contains lightbox markup and related CSS classes, but no gallery is
currently rendered and no lightbox interaction is implemented in JavaScript.
These can be used later if a featured photo gallery is added.

## SEO and social previews

`index.html` includes:

- Document title
- Meta description and keywords
- Search-engine indexing directive
- Open Graph title, description, image, URL, and site name
- Twitter summary-card metadata

Before deploying to a different domain or repository, update `og:url`. For the
most reliable social previews, change `og:image` and `twitter:image` to absolute
public URLs after the final GitHub Pages address is known.

## Deploy to GitHub Pages

The site is intended for:

```text
https://nohead13.github.io/nohead13.github.io/
```

For a repository named `nohead13.github.io`:

1. Copy the contents of `lending-page/` to the repository root.
2. Commit and push `index.html`, `style.css`, `script.js`, `assets/`, and
   `content/`.
3. Open the GitHub repository settings.
4. Select **Pages** under **Code and automation**.
5. Under **Build and deployment**, select **Deploy from a branch**.
6. Select the publishing branch, usually `main`, and the `/ (root)` folder.
7. Save and wait for GitHub Pages to publish the site.

Because all asset paths are relative, the project can also be deployed under a
project subdirectory without rebuilding it.

## Pre-deployment checklist

- Confirm every action and social URL opens the intended destination.
- Verify the event-order email address and PayPal link.
- Check the page at narrow mobile and desktop widths.
- Confirm the profile image is optimized for the web.
- Update the canonical Open Graph URL and image URLs.
- Test keyboard navigation and visible focus states.
- Run a Lighthouse audit for accessibility, SEO, and performance.
- Remove macOS `.DS_Store` files before publishing.

## Original specification

The initial design and feature request is retained in
`PROJECT_LENDING_PAGE_DOCUMENTATION.md`. It is useful as background and for
possible future enhancements, but when it conflicts with the current HTML,
CSS, or JavaScript, the implemented code takes priority.
