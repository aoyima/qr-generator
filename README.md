# Free QR Generator — GITLY

A single-file, client-side QR code generator. Live at **[qr.gitly.cc](https://qr.gitly.cc/)**.

Everything runs in the browser — no backend, no sign-up, no watermark, no tracking. Your input never leaves the page.

## Features

- **Generate** a QR code from any URL or text (press Enter or click the button).
- **Output size** for PNG export: 256, 512, 1024, or 2048 px.
- **Error correction** levels L (7%), M (15%), Q (25%), H (30%) — higher levels tolerate more damage/obstruction but hold less data.
- **Colors** — pick any foreground and background color.
- **Module style** — square, rounded, or dots.
- **Eye style** — square, rounded, or circle for the three corner finder patterns.
- **Margin** — quiet-zone border in pixels (0–64), applied exactly to PNG output.
- **Transparent background** — export with no background fill.
- **Live preview** updates as you adjust any visual option.
- **Download** as PNG (canvas-rendered) or SVG (vector) — your styling applies to both.
- **History** — the last 50 codes you generate, with thumbnails. Click one to restore its settings, re-download it as PNG/SVG, delete it, or clear all.
- **Responsive** — collapses to a single column on narrow screens; long URLs won't break the layout.

## How to use

1. Type or paste a URL or text into the content box.
2. (Optional) Adjust size, error correction, colors, styles, and margin.
3. Press **Enter** or click **Generate QR Code**.
4. Click **PNG** or **SVG** to download.

### Which format?

- **PNG** — a fixed-resolution raster image. Best for direct use in documents, slides, or web pages where you want a specific pixel size.
- **SVG** — vector; scales to any size without quality loss. Best for print or when the code may be resized later.

## Tech

- Plain HTML, CSS, and vanilla JavaScript in one `index.html` file. No build step.
- QR encoding via [`qrcode-generator`](https://cdnjs.com/libraries/qrcode-generator) (v1.4.4) loaded from cdnjs, with UTF-8 encoding enabled for unicode/emoji content.
- PNG is drawn to a `<canvas>`; SVG markup is built directly so custom module and eye shapes render identically in both.

## Deploy

Hosted as a static site:

1. Push/upload `index.html` to the `qr-generator` GitHub repo.
2. Cloudflare Pages is connected to the repo (no build command) and auto-deploys on every commit.
3. The custom domain `qr.gitly.cc` is configured under Pages → Custom domains.

To update: replace `index.html` in the repo and Cloudflare redeploys automatically.

## Notes & limitations

- **History is in-memory only.** It resets when you reload the page (nothing is saved to disk or the cloud).
- **Quiet zone.** A 0 px margin removes the quiet zone. The QR spec recommends roughly a 4-module border for reliable scanning; with no margin — especially on a transparent background — some scanners may struggle.
- **Contrast.** Very low foreground/background contrast can make a code unscannable. Keep the foreground clearly darker than the background.
- **Circle eye style** deviates from the QR spec and may fail on older or stricter scanners. Test before printing at scale.
- **Margin in pixels** is relative to the selected PNG size, so the same px value looks proportionally larger on a 256 px export than a 2048 px one.

Always scan-test a generated code before using it in production.
