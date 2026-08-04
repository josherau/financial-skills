# HTML Deck Style Guide

## Design intent

The final deck should feel like a repeatable CFO Monthly Financial Review.

It should not look like a generic AI dashboard. It should be clean, structured, restrained, and decision-ready.

## Company style

Use the active Project instructions as the source for company-specific style:

- Company name.
- Brand colors.
- Visual tone.
- Preferred labels.
- Audience.
- Materiality thresholds.
- Internal terminology.

If Project instructions do not define style, use the default CFO-neutral design system below.

## Repeatable structure

Every monthly deck must use the same order:

1. Cover and Executive Summary
2. Performance Scorecard
3. Revenue or Value Driver Quality
4. Margin and Profit Conversion
5. Cash and Working Capital
6. Management Agenda
7. Appendix

Use the same section names, CSS classes, page rhythm, and visual hierarchy each month.

## Default CFO-neutral design system

Use CSS variables:

```css
:root {
  --paper: #F7F5EF;
  --panel: #FFFFFF;
  --ink: #202421;
  --muted: #6B7280;
  --line: #D9DDD6;
  --grid: #ECEFEB;
  --accent: #344E41;
  --accent-soft: #A3B18A;
  --amber: #B7791F;
  --red: #9B2C2C;
  --bluegray: #5C6F7B;
}
```

Use colors sparingly:

- Accent: section labels, selected signal, subtle brand reinforcement.
- Amber: watch item.
- Red: material downside or risk.
- Gray: normal operating data.
- Off-white: page background.

## Typography

Use system fonts only.

Recommended stack:

`Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`

Use:

- Large concise headlines.
- Small uppercase section labels.
- Compact tables.
- Strong number hierarchy.
- Enough whitespace, but no decorative emptiness.

## Number formatting

Use consistent formatting:

- Revenue and costs: `$4.8M`, `$420K`
- Percentages: `42.1%`
- Basis points: `+120 bps`, `(80 bps)`
- Unfavorable values: brackets, for example `($120K)` or `(2.4%)`
- Favorable values: plus sign when helpful, for example `+$280K`

Do not mix `$000s`, full dollars, and millions on the same page unless explicitly labeled.

## Page layout

Each section should be a slide-like page inside the HTML.

Use:

```html
<section class="slide slide-summary">
  <div class="slide-kicker">Monthly Financial Review</div>
  <h1>...</h1>
</section>
```

Recommended fixed elements:

- Header: company name, MFR, month.
- Footer: source files and "Draft for management review".
- Page number or section label.

## Visual component classes

Use these repeatable classes:

- `.deck`
- `.slide`
- `.slide-header`
- `.slide-kicker`
- `.slide-meta`
- `.metric-grid`
- `.metric-card`
- `.metric-value`
- `.metric-delta`
- `.signal-positive`
- `.signal-watch`
- `.signal-risk`
- `.variance-table`
- `.bridge`
- `.bar-track`
- `.bar-fill`
- `.sparkline`
- `.agenda-table`
- `.footnote`
- `.assumption`
- `.source-note`

## Executive summary page

Include:

- One headline that tells the story.
- Three key messages.
- Three management questions.
- One small scorecard row.

Avoid:

- Long paragraphs.
- Generic "overall performance was mixed" unless supported.
- Marketing copy.

## Scorecard page

Use metrics relevant to the company, such as:

- Revenue or ARR.
- Gross margin or contribution margin.
- EBITDA, operating income, or cash burn.
- Cash balance.
- Working capital.
- Headcount.
- Core operating driver.

Show actual and comparison. Use exception flags only where material.

## Revenue or value driver page

Show:

- Driver chart or bridge.
- Segment, product, channel, region, customer, or usage table.
- The selected narrative from the user’s review answer.

## Margin and profit conversion page

Show:

- Profit conversion bridge.
- Margin read.
- What is confirmed vs uncertain.

## Cash and working capital page

Show:

- Cash bridge or movement table.
- Working capital signals.
- Interpretation and follow-up.

## Management agenda page

Show:

- Decisions required.
- Follow-ups.
- Owners where context supports it.
- Evidence to check next month.

## Appendix page

Show:

- Source workbooks.
- Period.
- Assumptions.
- Data gaps.
- User choices from each review cycle.

## HTML rules

- Standalone HTML only.
- Inline CSS.
- Inline SVG or CSS for charts.
- No external assets.
- No external JavaScript.
- No hidden data dumps.
- Use print-friendly CSS with page breaks.
