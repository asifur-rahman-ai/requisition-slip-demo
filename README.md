# AI Requisition Slip

A single-file, client-side **requisition slip generator**. It replaces two
paper slip formats with one smart web form: fill it in, get the total and the
amount in words automatically, then print it or save it as a PDF.

**[▶ Live demo](https://asifur-rahman-ai.github.io/requisition-slip-demo/)**
&nbsp;·&nbsp; all data in the demo is fictional.

<!-- Optional: add a screenshot to /screenshots and uncomment
![Preview](screenshots/preview.png)
-->

## Features

- **One form, two use cases** — Recipient and Date are always visible; an
  expandable section adds File No., Suit No. and Vessel Name for case-based
  requisitions
- **Dynamic particulars table** — add or remove line items, each with a
  cash/cheque reference and an amount
- **Live total** — recalculated as you type
- **Amount in words** — generated automatically, using Crore / Lakh /
  Thousand grouping (e.g. *Taka One Thousand Nine Hundred Twenty Six Only*)
- **Print** — builds a clean, standalone print document in a hidden iframe,
  so the printout contains only the slip and never the surrounding page
- **Download PDF** — client-side export (html2canvas + jsPDF), JPEG
  compressed so files stay small
- **Responsive** — the particulars table turns into stacked cards on phones
- **Design** — sharp-edged, glassmorphism-inspired UI with a single accent
  colour (`#2596be`)

## Privacy

Everything runs in the browser. There is no backend, no database, no
analytics and no network request carrying your input. Refreshing the page
clears the form.

## Tech

- Plain HTML, CSS and vanilla JavaScript — one file, no build step
- [jsPDF](https://github.com/parallax/jsPDF) `2.5.1` and
  [html2canvas](https://github.com/niklasvh/html2canvas) `1.4.1`, loaded from
  cdnjs (only needed for *Download PDF*; *Print* works without them)

## Run locally

Open `index.html` in any modern browser. No install required.

## Use it inside WordPress / Elementor

1. Open `index.html` and copy everything from `<div id="ars-root">` down to
   the final `</script>` (leave out the `<html>`, `<head>` and `<body>` tags
   and the demo banner).
2. In Elementor, add a **Custom HTML** widget and paste it in.
3. Replace `YOUR COMPANY NAME LIMITED` with your organisation's name — there
   are two places: the page header and the print template. Also change the
   PDF filename prefix near `pdf.save(`.

All styles are scoped under `#ars-root` and use `!important` on text colours,
so theme styles don't override them.

## Customise

| What | Where |
|---|---|
| Accent colour | `--accent` / `--accent-dark` at the top of the `<style>` block |
| Company name | Header markup, print template, PDF filename |
| Signature space | `.ars-sign-space` height |
| Currency wording | `amountToWords()` |

## Roadmap

- Optional auto-save of submitted slips (Google Sheets via Apps Script)
- Saved history / reprint of earlier slips

## Hosting on GitHub Pages

This demo is served with GitHub Pages straight from the `main` branch
(`Settings → Pages → Deploy from a branch → main / (root)`):

<https://asifur-rahman-ai.github.io/requisition-slip-demo/>

To publish your own copy, fork or clone the repo, enable Pages the same way,
and your site will be available at `https://<username>.github.io/<repo>/`.
