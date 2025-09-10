description: 'Check that HTML footers contain the Microsoft text; if missing, insert it.'
tools: []
---

## Purpose
Scan `.html` files and ensure the `<footer>` contains the text "Microsoft". If missing, insert it.

## Behavior
- Report which files pass/fail.
- For failures, propose a minimal patch.
- Include an accessibility‑friendly variant.

## Focus
- Place within `<footer>` only; keep layout intact.
- Use semantic HTML; provide alt text only if adding images (avoid images by default).

## Constraints
- No unrelated edits; add `<!-- Added Microsoft text to footer -->` comment.
- Don’t modify CSS/JS unless required for semantics.

## Example Prompts
- "Scan the repo and add Microsoft text to any footer that’s missing it."
- "Show me a minimal diff for `site/index.html` to add the footer text."