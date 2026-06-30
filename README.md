# PDF Footer Remover — a Claude Skill

Strip footers, watermark text, and "Created using X" branding strips from any PDF — directly inside Claude, no manual editing required.

Built this after manually editing the same Resumonk watermark off five different resume versions. One install later, it's a one-line request.

## What it does

Give Claude a PDF and ask it to remove the footer. It will:
1. Inspect the page to detect where the footer sits
2. Permanently redact that strip (not just visually crop it — it's gone from the content layer)
3. Verify the rest of your document is untouched
4. Hand you back a clean PDF

Works on multi-page documents, resumes, reports, or any PDF with a recurring bottom-of-page strip.

## Before / After

| Before | After |
|---|---|
| Resume with `Created using Resumonk - Online Resume Builder` on every page | Same resume, footer completely gone, formatting and layout untouched |

## Install

1. Download [`pdf-footer-remover.skill`](./pdf-footer-remover.skill) from this repo
2. In Claude, go to **Settings → Capabilities → Skills**
3. Click **Install skill** and select the downloaded file
4. Done — Claude will now use it automatically whenever you ask to remove a footer/watermark from a PDF

## Usage

Just upload a PDF and ask naturally:

> "Remove the footer from this PDF"
> "Clean up the Resumonk watermark on my resume"
> "Strip the bottom branding from this document"

No special syntax needed — the skill triggers on natural language.

## How it works

Under the hood, the skill uses [PyMuPDF](https://pymupdf.readthedocs.io/) to:
- Locate text blocks near the bottom of each page
- Apply a redaction annotation over that region (white fill)
- Flatten the redaction so the footer text is permanently removed, not just hidden

This is more robust than simply cropping the page (which can hide content without truly deleting it) — once redacted, the footer won't reappear in any PDF viewer.

## Limitations

- Tuned by default for a ~24pt-tall footer strip on standard Letter/A4 pages (792pt height). For unusual page sizes or taller footers, the skill re-inspects each PDF and adjusts.
- Designed for text-based footers. Image-based watermarks across the whole page (not a bottom strip) aren't covered by this skill.

## License

MIT — use it, fork it, improve it.

## Contributing

Found a PDF layout this doesn't handle well? Open an issue or PR with a sample (redact any personal info first).
