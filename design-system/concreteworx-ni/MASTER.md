# Design System Master File

> **LOGIC:** When building a specific page, first check `design-system/pages/[page-name].md`.
> If that file exists, its rules **override** this Master file.
> If not, strictly follow the rules below.

---

**Project:** ConcreteWorx NI
**Generated:** 2026-08-10 21:57:41 (ui-ux-pro-max `--design-system`)
**Overridden:** 2026-08-10 — colors and typography replaced with locked brand CI values (see [[Visual Identity]], [[Brand Voice]]). The tool's auto-picked palette/fonts were generic (terracotta+green "Plant Care Tracker" match) and did not reflect the actual brand; style direction ("Nature Distilled" per manual `--domain style` search) and spacing/shadow/component mechanics were kept as they matched well.
**Category:** Handcrafted Garden Ornaments E-commerce (WooCommerce)

---

## Global Rules

### Color Palette — Locked Brand CI (do not substitute)

| Role | Hex | CSS Variable | Source |
|------|-----|--------------|--------|
| Primary (Nature & Trust) | `#154734` Deep Forest Green | `--color-primary` | [[Visual Identity]] |
| On Primary | `#F7F7F7` | `--color-on-primary` | derived |
| Secondary (Grit & Material) | `#404648` Solid Slate Gray | `--color-secondary` | [[Visual Identity]] |
| Accent/CTA | `#CC5500` Earthy Terracotta | `--color-accent` | [[Visual Identity]] |
| Background | `#F7F7F7` Light Stone White | `--color-background` | [[Visual Identity]] |
| Foreground | `#1C1917` (near-black, warm) | `--color-foreground` | derived, WCAG-safe on `#F7F7F7` |
| Card | `#FFFFFF` | `--color-card` | derived |
| Muted | `#E9E7E3` | `--color-muted` | derived, warm-neutral |
| Border | `#D8D4CE` | `--color-border` | derived |
| Destructive | `#DC2626` | `--color-destructive` | standard |
| Ring | `#CC5500` | `--color-ring` | matches accent for visible focus |

**Color Notes:** These four hex values are the approved brand standard — see [[Visual Identity]]. Deep Forest Green anchors structure/nav, Slate Gray recedes as a secondary/background-adjacent tone so colourful product photography stands out, Terracotta is reserved for CTAs ("Order Now via WhatsApp") and interactive accents, Stone White is the primary background.

### Typography — Locked Brand CI (do not substitute)

- **Heading Font:** Playfair Display (traditional serif) — H1/H2, titles, section headers
- **Body Font:** Open Sans (modern sans-serif) — paragraphs, product descriptions, nav, CTAs
- **Mood:** timeless, elegant, legible, handcrafted-but-premium
- **Source:** [[Visual Identity]]
- **Google Fonts:** [Playfair Display + Open Sans](https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;500;600;700&family=Playfair+Display:wght@400;500;600;700&display=swap)

**CSS Import:**
```css
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;500;600;700&family=Playfair+Display:wght@400;500;600;700&display=swap');
```

**Tailwind Config:**
```js
fontFamily: {
  serif: ['Playfair Display', 'serif'],
  sans: ['Open Sans', 'sans-serif'],
}
```

### Spacing Variables

| Token | Value | Usage |
|-------|-------|-------|
| `--space-xs` | `4px` / `0.25rem` | Tight gaps |
| `--space-sm` | `8px` / `0.5rem` | Icon gaps, inline spacing |
| `--space-md` | `16px` / `1rem` | Standard padding |
| `--space-lg` | `24px` / `1.5rem` | Section padding |
| `--space-xl` | `32px` / `2rem` | Large gaps |
| `--space-2xl` | `48px` / `3rem` | Section margins |
| `--space-3xl` | `64px` / `4rem` | Hero padding |

### Shadow Depths

| Level | Value | Usage |
|-------|-------|-------|
| `--shadow-sm` | `0 1px 2px rgba(21,71,52,0.06)` | Subtle lift |
| `--shadow-md` | `0 4px 6px rgba(21,71,52,0.10)` | Cards, buttons |
| `--shadow-lg` | `0 10px 15px rgba(21,71,52,0.12)` | Modals, dropdowns |
| `--shadow-xl` | `0 20px 25px rgba(21,71,52,0.16)` | Hero images, featured product cards |

*Shadows are tinted with the primary Forest Green rather than pure black — a warmer, more "earthen" shadow consistent with the natural-materials aesthetic.*

---

## Component Specs

### Buttons

```css
/* Primary Button — "Order Now via WhatsApp" and other high-visibility CTAs */
.btn-primary {
  background: #CC5500;
  color: #FFFFFF;
  padding: 12px 24px;
  border-radius: 6px;
  font-family: 'Open Sans', sans-serif;
  font-weight: 600;
  transition: all 200ms ease;
  cursor: pointer;
}

.btn-primary:hover {
  background: #B34A00;
  transform: translateY(-1px);
}

/* Secondary Button */
.btn-secondary {
  background: transparent;
  color: #154734;
  border: 2px solid #154734;
  padding: 12px 24px;
  border-radius: 6px;
  font-family: 'Open Sans', sans-serif;
  font-weight: 600;
  transition: all 200ms ease;
  cursor: pointer;
}

.btn-secondary:hover {
  background: #154734;
  color: #FFFFFF;
}
```

### Product Cards

```css
.product-card {
  background: #FFFFFF;
  border: 1px solid #D8D4CE;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: var(--shadow-md);
  transition: all 200ms ease;
  cursor: pointer;
}

.product-card:hover {
  box-shadow: var(--shadow-lg);
  transform: translateY(-2px);
  border-color: #CC5500;
}

.product-card__image {
  aspect-ratio: 1 / 1;
  object-fit: cover;
  background: #E9E7E3; /* placeholder while loading */
}

.product-card__title {
  font-family: 'Playfair Display', serif;
  font-size: 1.125rem;
  color: #154734;
  margin: 12px 16px 4px;
}

.product-card__price {
  font-family: 'Open Sans', sans-serif;
  font-weight: 600;
  color: #404648;
  margin: 0 16px 16px;
}
```

Rationale: square product photography dominates the card (concrete ornaments photograph best face-on against a neutral background); serif title reinforces "timeless style" positioning at the point of decision; price stays in Slate Gray so it doesn't compete visually with the Terracotta "Add to basket" / CTA button.

### Inputs

```css
.input {
  padding: 12px 16px;
  border: 1px solid #D8D4CE;
  border-radius: 6px;
  font-family: 'Open Sans', sans-serif;
  font-size: 16px;
  transition: border-color 200ms ease;
}

.input:focus {
  border-color: #CC5500;
  outline: none;
  box-shadow: 0 0 0 3px #CC550033;
}
```

### Modals

```css
.modal-overlay {
  background: rgba(21, 71, 52, 0.55); /* forest-tinted overlay, not pure black */
  backdrop-filter: blur(4px);
}

.modal {
  background: #FFFFFF;
  border-radius: 12px;
  padding: 32px;
  box-shadow: var(--shadow-xl);
  max-width: 500px;
  width: 90%;
}
```

---

## Style Guidelines

**Style:** Nature Distilled *(from `ui-ux-pro-max --domain style "rustic earthy handcrafted artisan natural organic"`, chosen over the tool's auto-picked "Organic Biophilic" as the closer match for artisan/handmade positioning)*

**Keywords:** Muted earthy tones, wood/soil/sand/terracotta, warmth, organic materials, handmade warmth

**Best For:** Artisan goods, sustainable products, home decor, craft brands — directly applicable to handcrafted concrete garden ornaments

**Key Effects:** Subtle parallax on hero imagery, natural easing (`ease-out`), soft shadows (see shadow tokens above), light texture overlays only where they don't hurt legibility of product photography

### Page Pattern

**Pattern Name:** Feature-Rich Showcase (per [[Site Structure]] — matches the already-established homepage outline)

- **CTA Placement:** Above fold + persistent "Order Now via WhatsApp" access
- **Section Order:** Hero → "Explore Our Catalogue" tiles → Craft & Quality → Gallery/Social proof → Direct Contact CTA → Footer

---

## Anti-Patterns (Do NOT Use)

- ❌ Mixing in cool-toned blues/purples — stay within the earthy palette
- ❌ Overly rounded/pill-shaped buttons — soft (6-8px) radius fits "grit," not app-like full-pill radius
- ❌ Stock-photo gloss/studio-white product shots — product imagery should read as handcrafted, natural setting where possible

### Additional Forbidden Patterns

- ❌ **Emojis as icons** — Use SVG icons (Heroicons, Lucide, Simple Icons)
- ❌ **Missing cursor:pointer** — All clickable elements must have cursor:pointer
- ❌ **Layout-shifting hovers** — Avoid scale transforms that shift layout
- ❌ **Low contrast text** — Maintain 4.5:1 minimum contrast ratio (verify Slate Gray `#404648` on Stone White `#F7F7F7` for body text — passes AA)
- ❌ **Instant state changes** — Always use transitions (150-300ms)
- ❌ **Invisible focus states** — Focus states must be visible for a11y (use Terracotta ring, see `--color-ring`)

---

## Pre-Delivery Checklist

Before delivering any UI code, verify:

- [ ] No emojis used as icons (use SVG instead)
- [ ] All icons from consistent icon set (Heroicons/Lucide)
- [ ] `cursor-pointer` on all clickable elements
- [ ] Hover states with smooth transitions (150-300ms)
- [ ] Light mode: text contrast 4.5:1 minimum
- [ ] Focus states visible for keyboard navigation (Terracotta ring)
- [ ] `prefers-reduced-motion` respected
- [ ] Responsive: 375px, 768px, 1024px, 1440px
- [ ] No content hidden behind fixed navbars
- [ ] No horizontal scroll on mobile
- [ ] Only brand colors used — no substituted palette from generic tool output
- [ ] Playfair Display used for headings only, never body copy (legibility)

---

## See also
- [[Visual Identity]] — canonical brand palette & typography source
- [[Brand Voice]] — "Grit & Grandeur" copy tone this UI should reinforce
- [[Site Structure]] — nav and homepage section order this pattern implements
