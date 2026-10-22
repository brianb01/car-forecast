# Car Planning

A one-page plan for future car purchases: the car I own now, and the cars I'm looking for,
grouped by the year I expect to be ready to buy and the budget for that year.

**Live page:** https://brianb01.github.io/car-forecast/

## How the page is organized

- **Nav bar:** the total number of cars and years, and a button that switches between light
  and dark (your choice is remembered in this browser).
- **Available for trade:** the car I have now. Tap it to see its details.
- **Budget by year:** one button per target year with its budget range and a bar showing how
  it compares. Click a button to open or close that year.
- **Target YEAR | $budget:** one section per year. Each heading means "by this year, this
  is what I can spend". A car is listed under the budget that matches what it costs **today**;
  no attempt is made to predict depreciation. The nearest year starts open; later years start
  closed.
- Each car shows its make and model. Tap or click it to see the details: years, trim,
  must-have options, and the colors I want or want to avoid, each as a color dot with its
  name.
- A year with nothing in it yet stays on the page as a placeholder.

On a wide screen (992px and up) the owned car and the budget buttons stay pinned in a column
on the left while the year sections scroll on the right; narrower screens show everything
in one column. On large monitors the whole page scales up, text included, as if zoomed, so
it fills the screen. All sizes in the stylesheet are in `rem` for that reason.

The design was made in Claude Design ("Car Planning v2") and is built on Bootstrap 5.3.

## Files

- `index.html` — the whole site. One HTML file: Bootstrap 5.3 and Bootstrap Icons (from the
  jsdelivr CDN) do the layout, a single `<style>` block at the top holds the page's own
  styles, and a few lines of JavaScript at the bottom keep the budget buttons in step with
  the year sections and run the light/dark switch. The car entries and year sections open and
  close without JavaScript. The Geist font comes from Google Fonts; the page falls back to
  system fonts without it. No build step.

## Editing

Edit `index.html` directly. To add a car, copy an existing car's whole
`<details class="list-group-item p-0 car">` block into the right year's
`<div class="list-group">`, then change its text:

```html
<details class="list-group-item p-0 car">
  <summary class="list-group-item-action d-flex align-items-center gap-3 px-3 py-3 text-body">
    <div class="flex-grow-1 min-w-0">
      <div class="text-uppercase text-body-secondary fw-medium make">Ferrari</div>
      <div class="fw-semibold">488 Spider</div>
    </div>
    <i class="bi bi-chevron-down text-body-secondary chev"></i>
  </summary>
  <div class="px-3 pb-3 pt-1 bg-body-tertiary border-top">
    <dl class="row mb-0 pt-2">
      <dt class="col-sm-3 fw-medium text-body-secondary text-uppercase spec-k">Year</dt><dd class="col-sm-9 mb-3 spec-v">2017+ (avoiding the 2016 first model year)</dd>
      ...
    </dl>
  </div>
</details>
```

- The make goes in `.make`; everything else (model, generation) goes in the line below it.
- Add only the spec rows that apply (`Year`, `Trim`, `Transmission`, `Must have`,
  `Exterior`, `Interior`, ...). Copy a whole `dt`/`dd` pair from another car rather than
  retyping the classes.
- **Colors:** each wanted color is a pill (`color-chip`) holding a `<span class="dot NAME">`
  and the color's name. The available dot names are the `.dot.NAME` rules in the `<style>`
  block; to use a new color, add a rule there with its hex.
- **Avoid:** colors to avoid go at the end of the row they qualify, as an "Avoid" label
  followed by one amber pill per color.
- **Counts:** adding or removing a car changes two things by hand: the year's `.year-count`
  ("4 cars") and the total in the nav bar (`#summary`, "16 cars · 7 years").
- When the first car goes into an empty year, replace its "No cars picked yet." box with a
  `<div class="list-group list-group-flush border-top">`, and the reverse when the last car
  is removed.
- A new year needs a section, a budget button, a `.ladder .col:nth-child(N)` rule setting its
  bar width, and updates to the total and the header's year range.
- Escape `&` as `&amp;` and `<` as `&lt;`.

## Publishing

The site is served by GitHub Pages from the root of the `main` branch. Every push to `main`
redeploys it, usually within a few minutes. Check progress on the repo's **Actions** tab,
then reload the live page to confirm the change.
