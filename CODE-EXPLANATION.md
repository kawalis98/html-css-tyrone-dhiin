# Code Explanation

How the Rainy Days site works.

---

## Structure

7 HTML pages share one CSS file (`style.css`).

| Page | What it does |
|------|-------------|
| `index.html` | Hero, featured jackets, features, banner, newsletter |
| `shop.html` | Product grid with filters and sorting |
| `product.html` | Gallery, options, details, related products |
| `cart.html` | Cart items, order summary, related products |
| `checkout.html` | Contact, shipping, payment forms |
| `success.html` | Order confirmation |
| `placeholder.html` | "Coming Soon" for JS-required features |

**Why one CSS file?** All pages share the same header, footer, buttons, and cards. One file keeps it DRY.

---

## CSS-Only Interactivity (No JavaScript)

### Mobile Hamburger Menu

```html
<input type="checkbox" id="menu-toggle" class="menu-toggle-check">
<label for="menu-toggle" class="mobile-menu-btn">
  <span class="menu-lines"></span>
</label>
```

1. The checkbox is hidden.
2. The label is styled as a hamburger icon (3 lines from one span + `::before`/`::after`).
3. Tapping the label toggles the checkbox.
4. CSS shows/hides the nav:
   ```css
   .menu-toggle-check:checked ~ nav { display: block; }
   ```

### Cart Badge

```css
body:has(.cart-toggle-check:checked) .cart-badge {
  display: flex;
}
```

Clicking an "Add to Cart" label checks a hidden checkbox. `:has()` finds the badge inside the body and reveals it.

---

## Responsive Design

| Breakpoint | What Changes |
|------------|--------------|
| `max-width: 1024px` | Tablet: 2-column grids, sidebar unstuck |
| `max-width: 768px` | Small tablet: nav shrinks, hero text smaller |
| `max-width: 600px` | Phone: per-page UI redesign |
| `max-width: 480px` | Narrow phone: final refinements |

**Page-specific mobile layouts:** Body classes (`home-page`, `shop-page`, `product-page`) scope mobile styles so each page gets its own layout without affecting others.

**Grid vs Flexbox:** Grid for 2D layouts (product grids, cart, footer). Flexbox for 1D alignment (header, gallery, buttons).

---

## Accessibility

- Semantic landmarks: `header`, `nav`, `main`, `section`, `aside`, `footer`
- Unique `<title>` and `<meta name="description">` on every page
- One `<h1>` per page
- Alt text on all images
- Keyboard focus styles: `outline: 3px solid var(--cta)`
- WCAG AA colour contrast
- `prefers-reduced-motion` support
