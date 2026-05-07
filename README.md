# BX Design System Case Study

A single self-contained HTML artifact documenting components, tokens, motion, accessibility, and grid behavior I built as a contractor for the Blackstone BX Design System.

Built without frameworks or external dependencies. Hosted on GitHub Pages and embedded into a Squarespace portfolio page via iframe.

## Live URLs

- **Source page (GitHub Pages):** https://dandy-clancy.github.io/BX-Case-Study/
- **Portfolio embed (Squarespace):** https://luckily-creative.com/blackstone

## Updating the artifact

1. Replace `index.html` at the root of this repo (drag-and-drop in the GitHub web UI overwrites by filename).
2. Commit. GitHub Pages rebuilds in 30–90 seconds.
3. Hard-refresh the Squarespace page (Cmd+Shift+R) to pull the fresh build through the iframe.

## Squarespace embed snippet

The artifact broadcasts its content height to its parent via `postMessage`, so the iframe auto-resizes without nested scrollbars. Drop this snippet into a single Code Block on the Squarespace page (delete any other native blocks on the page first):

```html
<style>
  .sqs-block-code, .sqs-block-code .sqs-block-content,
  .sqs-block-html, .sqs-block-html .sqs-block-content,
  .sqs-block-embed, .sqs-block-embed .sqs-block-content,
  .sqs-html-content { padding: 0 !important; margin: 0 !important; }
  .bx-cs-embed { margin: 0; padding: 0; line-height: 0; }
  .bx-cs-embed iframe {
    width: 100%;
    border: 0;
    display: block;
    min-height: 600px;
    background: #fff;
  }
</style>
<div class="bx-cs-embed">
  <iframe
    id="bx-cs-frame"
    src="https://dandy-clancy.github.io/BX-Case-Study/"
    title="BX Design System Case Study"
    loading="lazy">
  </iframe>
</div>
<script>
(function () {
  var frame = document.getElementById('bx-cs-frame');
  if (!frame) return;
  window.addEventListener('message', function (ev) {
    if (!ev.data || ev.data.type !== 'bx-cs-height') return;
    if (frame.contentWindow !== ev.source) return;
    var h = parseInt(ev.data.height, 10);
    if (h && h > 100) frame.style.height = h + 'px';
  });
})();
</script>
```

## What's inside

- Hero with light/dark theme toggle
- Tab nav: Overview, UI Components, Data Visualization, Typography, Color & Theme, Iconography, Motion, Responsive Grid, Tokens, Accessibility
- Sub-tabs inside UI Components: Buttons & Selectors, Image Blocks & Media, Dropdowns, Accordions & Lists, Tabs & Navigation, Forms & Inputs, Cards, Tables
- Audited typography (Sanomat for display, Guardian Sans for body), color tokens, motion tokens, 6-breakpoint responsive grid
- A token architecture cascade (Primitive → Semantic → Component) and a WCAG 2.1 AA contrast audit

## Working notes

The HTML is hand-authored, single-file, no build step. CSS uses custom properties for theming (`--bx-bg`, `--bx-fg`, `--bx-rule`, `--bx-rule-soft`). All animations honor `prefers-reduced-motion`. Card images use a three-act curtain reveal — page bg → black panel rises from below → image rises pushing curtain out the top.
