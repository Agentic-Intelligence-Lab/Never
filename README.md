# Never — Continual Learning Research Series

Landing page for the HKU Agentic Intelligence Lab research series. Paper cards and the month timeline are defined in [`index.html`](index.html) inside `.paper-list`.

## Adding a paper card

Copy one of the templates below into `.paper-list` in `index.html`. The left timeline is built automatically from `data-month` on each `.paper-entry` when the page loads—no manual timeline edits are required.

### Required attributes

| Attribute / class | Description |
|-------------------|-------------|
| `class="paper-entry"` | Marks the card for the timeline script |
| `id` | Unique scroll target on the page (see [Multiple papers in one month](#multiple-papers-in-one-month)) |
| `data-month="YYYY-MM"` | Month bucket for the timeline (ISO year-month); can be shared across cards |
| `<time datetime="YYYY-MM">` | Human-readable date shown on the card; should match `data-month` |

### Multiple papers in one month

Several cards can belong to the **same calendar month**. They all use the same `data-month` value; each card still needs its **own unique** `id`.

**How it works**

- The timeline shows **one label per month** (e.g. “May 2026”), not one label per card.
- Clicking that month scrolls to the **first** `.paper-entry` with that `data-month` in `.paper-list` (top to bottom in the HTML).
- While scrolling, any visible card with that month can highlight the same timeline label.

**Markup rules**

1. Use the **same** `data-month` on every card in that month (e.g. `data-month="2026-05"`).
2. Give **each** card a **different** `id`. Do not reuse `id="paper-2026-05"` on a second card.
3. Put the card you want the timeline click to land on **first** among same-month entries (or accept that the timeline always jumps to the first one).
4. Keep same-month cards **together** in the list so readers see them as a group.

**Recommended `id` pattern**

| Card | `id` | `data-month` |
|------|------|----------------|
| First paper in May 2026 | `paper-2026-05` | `2026-05` |
| Second paper in May 2026 | `paper-2026-05-2` | `2026-05` |
| Third (optional) | `paper-2026-05-3` | `2026-05` |

You can also use a short slug instead of a number, e.g. `paper-2026-05-vla` and `paper-2026-05-dataset`, as long as every `id` is unique.

**Example: two papers in May 2026**

```html
<!-- Timeline “May 2026” scrolls here (first in list for this month) -->
<article class="paper-entry" id="paper-2026-05" data-month="2026-05">
  <div class="paper-card">
    <!-- ... first paper ... -->
    <time class="paper-card-date" datetime="2026-05">May 2026</time>
  </div>
</article>

<!-- Same month; unique id; link directly with #paper-2026-05-2 -->
<article class="paper-entry" id="paper-2026-05-2" data-month="2026-05">
  <div class="paper-card">
    <!-- ... second paper ... -->
    <time class="paper-card-date" datetime="2026-05">May 2026</time>
  </div>
</article>
```

To link to the second card from elsewhere, use the hash that matches its `id`, e.g. `index.html#paper-2026-05-2`. The timeline month link still opens the **first** card (`#paper-2026-05`).

### Thumbnail images

- **Aspect ratio:** 16:9  
- **Recommended size:** 800×450 px (use 1200×675 or higher for sharper Retina / mobile)  
- **Format:** JPG or WebP  
- Images use `object-fit: cover`; keep important content near the center.

---

### Example: published paper (with optional links)

```html
<article class="paper-entry" id="paper-2026-05" data-month="2026-05">
  <div class="paper-card">
    <a class="paper-card-thumb" href="pages/paper-1.html">
      <img src="static/images/carousel1.jpg" alt="Short description of the figure" width="800" height="450" loading="lazy">
    </a>
    <div class="paper-card-content">
      <div class="paper-card-meta">
        <time class="paper-card-date" datetime="2026-05">May 2026</time>
        <div class="paper-card-authors">
          <span>First Author</span>
          <span>Second Author</span>
          <span>Agentic Intelligence Lab, HKU</span>
        </div>
      </div>
      <h2 class="paper-card-title">
        <a href="pages/paper-1.html">Your Paper Title Goes Here</a>
      </h2>
      <p class="paper-card-abstract">
        One or two sentences summarizing the contribution, similar to an abstract lead.
      </p>
      <div class="paper-card-actions">
        <a class="paper-card-link" href="https://arxiv.org/abs/XXXX.XXXXX" target="_blank" rel="noopener">Paper</a>
        <a class="paper-card-link" href="pages/paper-1.html">Website</a>
        <a class="paper-card-link" href="https://github.com/org/repo" target="_blank" rel="noopener">Code</a>
      </div>
    </div>
  </div>
</article>
```

**Action links (all optional except what you need):**

- **Paper** — PDF, arXiv, or publisher page  
- **Website** — project page on this site or an external URL  
- **Code** — repository or demo  

Omit any link you do not need (e.g. only `Paper`, or `Paper` + `Code`).

Use `target="_blank" rel="noopener"` for external URLs.

---

### Example: coming soon (placeholder)

No thumbnail image; no action links. Uses `is-placeholder` to disable the card hover lift.

```html
<article class="paper-entry" id="paper-2026-09" data-month="2026-09">
  <div class="paper-card is-placeholder" role="note" aria-label="Placeholder for an upcoming paper">
    <div class="paper-card-thumb">
      <span class="paper-card-badge">Coming soon</span>
    </div>
    <div class="paper-card-content">
      <div class="paper-card-meta">
        <time class="paper-card-date" datetime="2026-09">September 2026</time>
        <div class="paper-card-authors">
          <span>Agentic Intelligence Lab, HKU</span>
        </div>
      </div>
      <h2 class="paper-card-title">Upcoming Project Title</h2>
      <p class="paper-card-abstract">
        Short teaser text for work that is not yet released.
      </p>
    </div>
  </div>
</article>
```

---

### Authors

List each author as its own `<span>`; commas are inserted automatically between spans:

```html
<div class="paper-card-authors">
  <span>Alice Smith</span>
  <span>Bob Jones</span>
  <span>Agentic Intelligence Lab, HKU</span>
</div>
```

---

### Checklist before publishing

- [ ] `data-month` and `<time datetime="...">` use the same `YYYY-MM`  
- [ ] Every card has a **unique** `id`; same-month extras use `paper-YYYY-MM-2`, etc.  
- [ ] If multiple cards share a month, the intended timeline target is **first** in `.paper-list` for that month  
- [ ] Thumbnail is 16:9 (800×450 or larger)  
- [ ] Title and thumbnail link to the project page (if applicable)  
- [ ] External links use `target="_blank" rel="noopener"`  
- [ ] Card is placed inside `<div class="paper-list">` in `index.html`
