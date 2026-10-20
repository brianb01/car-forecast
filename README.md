# Car Planning

A one-page plan for future car purchases: the car I own now, and the cars I'm looking for,
grouped by the year I expect to be ready to buy and the budget for that year.

**Live page:** https://brianb01.github.io/car-forecast/

## How the page is organized

- **Budget by year:** a small chart at the top with one column per target year, showing that
  year's budget range and how many cars are in it. Click a column to open or close that
  year; **Expand all / Collapse all** opens or closes every year at once.
- **Currently own:** the car I have now.
- **Target YEAR | $budget:** one section per year. Each heading means "by this year, this
  is what I can spend". A car is listed under the budget that matches what it costs **today**;
  no attempt is made to predict depreciation. The nearest year starts open; later years start
  closed.
- Each car shows its make, model, color swatches for the colors I want, and the model years
  I'm after. Tap or click it to see the details: years, trim, must-have options, and the
  colors I want or want to avoid.
- A year with nothing in it yet stays on the page as a placeholder.

The design is dark-only. It was made in Claude Design ("1c · Redesign — Dark").

## Files

- `index.html` — the whole site. One self-contained file: plain HTML with all styles in a
  single `<style>` block at the top and a few lines of JavaScript at the bottom that keep the
  budget chart and the Expand/Collapse button in step with the year sections. The car entries
  open and close without JavaScript. The only external resource is the Geist font from Google
  Fonts; the page falls back to system fonts without it. No build step.

## Editing

Edit `index.html` directly. To add a car, copy an existing entry inside the right year's
`<ul class="cars">`:

```html
<li><details class="car">
  <summary><span class="make">Ferrari</span><span class="model-wrap"><span class="model">488 Spider</span><span class="dots" aria-hidden="true"><span class="dot rosso-corsa" title="Rosso Corsa"></span><span class="dot light-blue" title="Light Blue"></span></span></span><span class="tag-slot"><span class="chip">2017+</span></span><svg class="chev" viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M5 8l5 5 5-5"/></svg></summary>
  <dl class="specs">
    <dt>Year</dt><dd>2017+ (avoiding the 2016 first model year)</dd>
    <dt>Exterior</dt><dd>Rosso Corsa (preferred)</dd>
    <dt>Interior</dt><dd>Cuoio, Sabbia, or Iroko
      <span class="avoid"><span class="avoid-label">Avoid</span><span class="avoid-chip"><span class="dot crema" title="Crema"></span>Crema</span></span></dd>
  </dl>
</details></li>
```

- The make goes in `.make`; everything else (model, generation) goes in `.model`.
- **Swatches:** each `<span class="dot NAME">` is a color. The available names are the
  `.dot.NAME` rules in the `<style>` block; to use a new color, add a rule there with its hex.
- **Year chip:** the short year range (`2017+`, `2010–12`) goes in `<span class="chip">`
  inside `.tag-slot`. With no year to show, leave `.tag-slot` empty but keep it.
- Add only the spec rows that apply (`Year`, `Trim`, `Transmission`, `Must have`,
  `Exterior`, `Interior`, ...).
- **Avoid:** colors to avoid go in a `<span class="avoid">` at the end of the row they
  qualify, as an "Avoid" label followed by one `avoid-chip` per color.
- **Counts:** adding or removing a car changes three numbers by hand: the year's
  `.year-count` ("4 cars"), the matching `.col-count` in the budget chart, and the total in
  `.ladder-sum` ("16 cars · 6 years").
- When the first car goes into an empty year, replace its `<p class="empty">` with a
  `<ul class="cars">`, and the reverse when the last car is removed.
- A new year needs a section, a chart column, and a `.col:nth-child(N)` rule placing its bar.
- Escape `&` as `&amp;` and `<` as `&lt;`.

## Publishing

The site is served by GitHub Pages from the root of the `main` branch. Every push to `main`
redeploys it, usually within a few minutes. Check progress on the repo's **Actions** tab,
then reload the live page to confirm the change.
