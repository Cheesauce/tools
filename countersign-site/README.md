# Countersign

A browser-only PDF signing tool.

Open a PDF, add a signature, initials, date or text, and download the signed copy. Signatures can be drawn, typed in a handwriting font, or uploaded as an image with automatic background removal. Saved signatures are kept in the browser for next time.

Everything runs on the user's own device. PDFs and signatures are never uploaded to a server.

> This adds a visual signature, the same as signing a printout. It is not a certificate-based digital signature (PAdES / PKI).

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The whole app: markup, styles and script |
| `assets/favicon.svg`, `assets/favicon.png` | Browser tab icon (the Countersign mark) |
| `assets/apple-touch-icon.png` | Home-screen icon |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

There is no build step and nothing to install. Libraries load from cdnjs:

- [pdf.js 3.11.174](https://mozilla.github.io/pdf.js/) renders the pages
- [pdf-lib 1.17.1](https://pdf-lib.js.org/) writes the signed PDF

Fonts load from Google Fonts.

## Run locally

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

Then go to http://localhost:8000.

## Publish on GitHub Pages

1. Create a repository under the `revlv-solutions` organization, for example `countersign`.
2. Push this folder's contents to the `main` branch:

   ```bash
   git init
   git add .
   git commit -m "Add Countersign PDF signer"
   git branch -M main
   git remote add origin https://github.com/revlv-solutions/countersign.git
   git push -u origin main
   ```

3. On GitHub, open **Settings > Pages**. Under **Build and deployment**, set **Source** to **Deploy from a branch**, choose `main` and `/ (root)`, then click **Save**.
4. After a minute the site is live at `https://revlv-solutions.github.io/countersign/`.

Check with the platform team before enabling Pages if your organization's policy requires it. Pages sites are public even when the repository is private on some plans.

## Notes

- Supported: Chrome, Edge, Safari and Firefox (current versions), desktop and mobile.
- Password-protected PDFs can't be opened. Remove the password first.
- Typed date and text fields use Helvetica in the PDF. Characters outside the standard Latin set are embedded as an image instead.
