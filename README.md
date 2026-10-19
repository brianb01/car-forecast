# Car Forecast

A one-page plan for future car purchases: the car I own now, and the cars I'm looking for,
grouped by the year I expect to be ready to buy and the budget for that year.

**Live page:** https://brianb01.github.io/car-forecast/

## How the page is organized

- **Currently own:** the car I have now.
- **Ready in YEAR | $budget:** one section per year. Each heading means "by this year, this
  is what I can spend". A car is listed under the budget that matches what it costs **today**;
  no attempt is made to predict depreciation.
- Each car shows only its make and model. Tap or click it to see the details: years,
  trim, must-have options, and the exterior and interior colors I want or want to avoid.
- A year with nothing in it yet stays on the page as a placeholder.

## Files

- `index.html` — the whole site. One self-contained file: plain HTML, with all styles in a
  single `<style>` block at the top. No JavaScript, no build step, no external dependencies.
  Light and dark mode follow the viewer's system setting.

## Editing

Edit `index.html` directly. To add a car, copy an existing entry inside the right section's
`<ul class="cars">`:

```html
<li><details>
  <summary><span class="make">Ferrari</span><span class="model">488 Spider</span>
    <svg class="chevron" viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M5 8l5 5 5-5"/></svg></summary>
  <dl class="specs">
    <dt>Year</dt><dd>2017+ (avoiding the 2016 first model year)</dd>
    <dt>Exterior</dt><dd>Rosso Corsa (preferred)</dd>
    <dt>Interior</dt><dd>Cuoio, Sabbia, or Iroko
      <span class="avoid">Beige Tradizione, Crema</span></dd>
  </dl>
</details></li>
```

- The make goes in `.make`; everything else (model, generation) goes in `.model`.
- Add only the spec rows that apply (`Year`, `Trim`, `Transmission`, `Must have`,
  `Exterior`, `Interior`, ...).
- Colors to avoid go in a `<span class="avoid">` inside the row they qualify. The page adds
  the "Avoid:" label itself, so don't type it.
- When the first car goes into an empty year, replace its `<p class="empty">` with a
  `<ul class="cars">`, and the reverse when the last car is removed.
- Escape `&` as `&amp;` and `<` as `&lt;`.

## Publishing

The site is served by GitHub Pages from the root of the `main` branch. Every push to `main`
redeploys it, usually within a few minutes. Check progress on the repo's **Actions** tab,
then reload the live page to confirm the change.
