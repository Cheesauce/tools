# Papeles

Browser-only PDF tools: sign, edit text, add fillable form fields, merge, split, OCR, and convert between images and PDF.

Open a PDF, add a signature, initials, date or text, and download the signed copy. Signatures can be drawn, typed in a handwriting font, or uploaded as an image with automatic background removal. Saved signatures are kept in the browser for next time.

Everything runs on the user's own device. PDFs and signatures are never uploaded to a server.

> This adds a visual signature, the same as signing a printout. It is not a certificate-based digital signature (PAdES / PKI).

## Files

| Path | What it is |
| --- | --- |
| `index.html` | The whole app: markup, styles and script |
| `assets/favicon.svg`, `assets/favicon.png` | Browser tab icon (the Papeles mark) |
| `assets/apple-touch-icon.png` | Home-screen icon |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

There is no build step and nothing to install. Libraries load from cdnjs:

- [pdf.js 3.11.174](https://mozilla.github.io/pdf.js/) renders the pages
- [pdf-lib 1.17.1](https://pdf-lib.js.org/) writes the signed PDF
- [JSZip 3.10.1](https://stuk.github.io/jszip/) bundles multi-file downloads
- [Tesseract.js 5.1.1](https://tesseract.projectnaptha.com/) runs OCR. It loads only when OCR is first used and downloads its engine and language data (about 5 to 15 MB) from jsDelivr.

Fonts load from Google Fonts.

## Run locally

Open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

Then go to http://localhost:8000.

## Publish on GitHub Pages

`index.html` must sit at the top level of the repository, not inside a folder. Upload the **contents** of this folder, not the folder itself. Leave out `claude-link/`, which only holds the copy used for the Claude artifact.

**With the GitHub website**

1. In the repository, click **Add file > Upload files**.
2. Drag in `index.html`, `README.md` and the `assets` folder, then click **Commit changes**.
3. In **Settings > Pages**, set **Source** to **Deploy from a branch**, choose `main` and `/ (root)`, then click **Save**.
4. After a minute the site is live at `https://<user>.github.io/<repository>/`.

**With git**

```bash
git init
git add .
git commit -m "Add Papeles PDF tools"
git branch -M main
git remote add origin https://github.com/<user>/<repository>.git
git push -u origin main
```

`.gitignore` already leaves out `claude-link/` and `.claude/`. Then enable Pages as in step 3.

Check with the platform team before enabling Pages if your organization's policy requires it. Pages sites are public even when the repository is private on some plans.

## Notes

- Supported: Chrome, Edge, Safari and Firefox (current versions), desktop and mobile.
- Password-protected PDFs can't be opened. Remove the password first.
- **Preview before download**: every tool shows the finished file first (all pages, the images, the files inside a zip, or the text) with **Back to editing** and **Download** buttons. Nothing is saved until you choose Download.
- **Search** (top bar, or Ctrl/Cmd+K) finds any tool by name, for example "jpg" or "combine", and finds text in the open PDF with highlighted matches. Scanned pages need OCR before their text can be found.
- **Formatting bar**: select any text, date or edited text to change its font (original, Helvetica, Times or Courier), size in points, bold, italic and colour, or to duplicate or delete it. **Hide tools / Show tools** collapses the left panel.
- **Checkbox** and **Fill-in field** are saved as real PDF form fields, so the downloaded file can be filled in with Acrobat, Preview or a browser.
- **Ctrl/Cmd+Z** undoes and **Ctrl/Cmd+Shift+Z** or **Ctrl+Y** redoes changes on the Sign tab.
- **OCR** works on the GitHub Pages site but not on the Claude preview link, which blocks the engine download. Results depend on scan quality, so check recognised text against the original.
- **Edit existing text** covers the old text with a patch matching the background and writes the new text at the same size with the PDF's own embedded font. Embedded fonts often contain only the letters the document already uses; if you type a letter that is missing, that line falls back to a similar standard font (Helvetica, Times or Courier) and the app tells you. The old text is hidden, not deleted: it can still be found by searching or copying, so don't use it to remove confidential information. Scanned PDFs have no editable text.
- Typed date and text fields use Helvetica in the PDF. Characters outside the standard Latin set are embedded as an image instead.
