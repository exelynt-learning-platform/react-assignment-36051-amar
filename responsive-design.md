# Responsive Web Design Fundamentals

A practical guide to understanding, planning, and building responsive web layouts.

---

## 1. What Is Responsive Web Design?

Responsive Web Design (RWD) is an approach to building websites so that a single
HTML document and stylesheet adapt to different screen sizes, resolutions, and
device capabilities. Instead of creating separate websites for phones, tablets,
and desktops, the layout responds to the available viewport width.

Responsive design combines three ideas:

- **Flexible layouts** that stretch, shrink, and reflow instead of using fixed widths.
- **Scalable media** such as images and videos that resize with their containers.
- **Media queries** that apply different styles at different screen sizes.

The goal is a consistent, readable, and usable experience on every device, from a
small phone to a large desktop monitor.

---

## 2. Why Responsive Layouts Are Important

- **Most traffic is mobile.** A large share of users browse on phones, so a layout
  that only works on desktop excludes many visitors.
- **One codebase is easier to maintain.** A single responsive site is simpler and
  cheaper to update than separate mobile and desktop versions.
- **Better user experience.** Content stays readable, navigation stays usable, and
  users do not need to pinch, zoom, or scroll sideways.
- **Improved accessibility.** Responsive layouts support zooming, reflow, and
  assistive technologies more reliably.
- **Better SEO.** Search engines favour mobile-friendly pages and use the mobile
  version of a page for indexing.
- **Future-friendly.** New screen sizes and devices appear constantly; a flexible
  layout adapts without a redesign.

---

## 3. Mobile-First vs Desktop-First

Both approaches produce responsive layouts, but they start from opposite ends and
use different CSS strategies.

### 3.1 Mobile-First Approach

**How it works**

1. Write the base CSS for the smallest screen (usually a phone).
2. Use `min-width` media queries to add layout complexity as the viewport grows.
3. Enhance the design progressively for tablets and desktops.

```css
/* Base styles: mobile */
.card {
  width: 100%;
  padding: 1rem;
}

/* Tablet and up */
@media (min-width: 768px) {
  .card {
    width: 50%;
  }
}

/* Desktop and up */
@media (min-width: 1200px) {
  .card {
    width: 33.333%;
  }
}
```

**Where it is commonly used**

- New websites and web applications.
- Content-focused sites such as blogs, news sites, and marketing pages.
- Projects built with mobile-first frameworks such as Bootstrap 5 and Tailwind CSS.
- Performance-sensitive products where mobile load speed matters.

**Advantages**

- Mobile styles are small and load first.
- Forces teams to prioritise content and essential features.
- Usually results in cleaner, simpler CSS.
- Matches the "progressive enhancement" mindset.

### 3.2 Desktop-First Approach

**How it works**

1. Write the base CSS for a large desktop screen.
2. Use `max-width` media queries to simplify the layout as the viewport shrinks.
3. Remove columns, reduce spacing, and stack content on smaller screens.

```css
/* Base styles: desktop */
.card {
  width: 33.333%;
}

/* Smaller desktops and tablets */
@media (max-width: 1199px) {
  .card {
    width: 50%;
  }
}

/* Phones */
@media (max-width: 767px) {
  .card {
    width: 100%;
  }
}
```

**Where it is commonly used**

- Legacy websites that were originally designed for desktop.
- Enterprise dashboards and internal tools with complex data tables.
- Design-led projects where the desktop layout is the primary reference.
- Websites with an existing desktop design system that must be preserved.

**Advantages**

- Natural fit when a desktop design already exists.
- Easier to adapt complex desktop interfaces without redesigning everything.
- Useful when most users are on large screens, such as internal business tools.

### 3.3 Comparison

| Topic | Mobile-First | Desktop-First |
| --- | --- | --- |
| Starting point | Smallest screen | Largest screen |
| Media query type | `min-width` | `max-width` |
| Strategy | Progressive enhancement | Graceful degradation |
| Default CSS | Simple, single-column | Complex, multi-column |
| Typical projects | New sites, public content, apps | Legacy sites, admin dashboards |
| Performance | Usually better on mobile | Can load heavier base CSS on mobile |

Modern best practice generally favours mobile-first, but desktop-first is still a
valid choice when a project starts from an existing desktop design.

---

## 4. Common Screen Sizes

Screen sizes below are written in **CSS pixels** (viewport width), not physical
device pixels. Actual device resolutions are often higher.

### Mobile

- **Small phones:** 320px – 360px wide
- **Common phones:** 375px, 390px, 414px wide
- **Large phones / small tablets:** 430px – 480px wide
- Typical portrait sizes: 360×640, 375×667, 390×844, 414×896

### Tablet

- **Small tablets:** 600px – 768px wide
- **Common tablets:** 768px, 810px, 820px wide
- **Large tablets:** 1024px wide
- Typical sizes: 768×1024, 820×1180, 1024×1366

### Desktop

- **Laptops:** 1280px – 1440px wide
- **Common desktop widths:** 1280×720, 1366×768, 1440×900, 1536×864
- **Large desktops:** 1600px, 1920×1080, 2560×1440 and above

> Always include `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
> so mobile browsers use the device width as the viewport instead of a zoomed-out
> desktop width.

---

## 5. Common CSS Breakpoints

A **breakpoint** is the viewport width at which a layout changes, usually through a
media query. There is no universal set of breakpoints, but these are widely used:

| Breakpoint | Typical target |
| --- | --- |
| `320px` | Small mobile phones |
| `375px` / `390px` | Common modern phones |
| `480px` | Large phones, small tablets in portrait |
| `576px` | Small tablets (Bootstrap `sm`) |
| `768px` | Tablets and tablet landscape (Bootstrap `md`) |
| `992px` | Small laptops and desktops (Bootstrap `lg`) |
| `1024px` | Tablets landscape and small desktops |
| `1200px` | Standard desktops (Bootstrap `xl`) |
| `1280px` | Large laptops and desktops |
| `1440px` | Large desktop monitors |
| `1536px` | Very large screens (Tailwind `2xl`) |

### How to Choose Breakpoints

- **Design to the content, not only to devices.** Resize the browser and add a
  breakpoint where the layout starts to look cramped or awkward.
- **Start with a small set.** Three to five well-chosen breakpoints are usually
  enough; too many make the CSS difficult to maintain.
- **Use mobile-first ranges.** Prefer `min-width` queries and order them from
  smallest to largest.
- **Remember landscape and zoom.** Users may rotate devices or zoom the page, so
  test beyond one orientation.

Example of a typical mobile-first breakpoint set:

```css
/* Base: mobile */
.container { padding: 1rem; }

/* Large phone / small tablet */
@media (min-width: 576px) {
  .container { padding: 1.5rem; }
}

/* Tablet */
@media (min-width: 768px) {
  .container { padding: 2rem; }
}

/* Desktop */
@media (min-width: 1024px) {
  .container {
    max-width: 1100px;
    margin: 0 auto;
    padding: 2.5rem;
  }
}
```

---

## 6. Core Responsive Design Principles

### 6.1 Flexible Layouts

Flexible layouts use relative units instead of fixed pixel widths so content can
reflow naturally.

- Use percentages, `fr` units, `minmax()`, and `max-width` instead of fixed widths.
- Use **Flexbox** for one-dimensional layouts (rows or columns).
- Use **CSS Grid** for two-dimensional page layouts.
- Allow content to wrap with `flex-wrap: wrap`.
- Avoid fixed heights on text containers; let content define height.

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1.5rem;
}

.page {
  width: min(1100px, 90%);
  margin-inline: auto;
}
```

### 6.2 Scalable Images and Media

Images and other media must never overflow their containers.

```css
img,
video {
  max-width: 100%;
  height: auto;
  display: block;
}
```

Additional techniques:

- Use `srcset` and `sizes` to serve appropriately sized images to different screens.
- Use the `<picture>` element when art direction is needed.
- Use `aspect-ratio` to reserve space and prevent layout shifts.
- Use `object-fit: cover` for consistent image framing.
- Avoid setting both fixed `width` and `height` without `height: auto`.

### 6.3 Media Queries

Media queries apply CSS only when certain conditions are true, such as a minimum
viewport width.

```css
@media (min-width: 768px) {
  .sidebar {
    display: block;
    width: 280px;
  }
}
```

- `min-width` = "this width and above" (mobile-first).
- `max-width` = "this width and below" (desktop-first).
- Modern CSS also supports range syntax: `@media (400px <= width <= 900px)`.
- Media queries can also respond to orientation, resolution, hover capability, and
  user preferences such as `prefers-reduced-motion` and `prefers-color-scheme`.

### 6.4 Additional Principles

- **Responsive navigation:** collapse links into a menu button on small screens.
- **Fluid typography:** use `clamp()` so headings scale smoothly between sizes.
- **Touch-friendly targets:** make buttons and links at least about 44×44 CSS pixels.
- **Readable line length:** limit text width to roughly 60–75 characters.
- **Test on real devices and browser dev tools:** check multiple widths, zoom levels,
  and orientations.

```css
h1 {
  font-size: clamp(1.75rem, 4vw, 2.75rem);
}
```

---

## 7. Real-World Example: BBC News

BBC News (bbc.com/news) is a well-known responsive website.

- The page uses a **fluid grid** that reflows from a single column on phones to
  multiple columns on desktop.
- **Images and video players scale** with their containers using fluid widths.
- **Navigation changes with screen size:** primary links collapse into a menu on
  smaller screens and expand into a horizontal bar on larger screens.
- **Content priority changes:** smaller screens show fewer secondary stories and
  simpler layouts, while desktops display more modules in a wider grid.
- **Typography and spacing adapt** so headlines and article text remain readable
  on every device.

Other widely referenced responsive examples include Wikipedia, GitHub, Airbnb, and
the GOV.UK website. Each adapts navigation, media, and content density across screen
sizes while keeping one codebase.

---

## 8. Responsive Design Checklist

- [ ] Viewport meta tag included in every page.
- [ ] Base styles written for small screens (mobile-first preferred).
- [ ] Layout uses Flexbox, Grid, percentages, and relative units.
- [ ] Images use `max-width: 100%` and `height: auto`.
- [ ] Breakpoints chosen based on content, not only on device names.
- [ ] Navigation is usable on small screens.
- [ ] Text remains readable without horizontal scrolling.
- [ ] Touch targets are large enough.
- [ ] Tested at common widths: 320, 375, 480, 768, 1024, 1280, 1440px.
- [ ] Tested in multiple browsers and with zoomed or enlarged text.

---

## Summary

Responsive web design is the practice of building one flexible website that works
well everywhere. Mobile-first and desktop-first are two valid strategies; mobile-first
is the most common default for new projects, while desktop-first remains useful for
legacy and data-heavy desktop tools. Combining flexible layouts, scalable media, and
well-chosen media queries produces interfaces that are readable, accessible, and
maintainable across mobile, tablet, and desktop screens.
