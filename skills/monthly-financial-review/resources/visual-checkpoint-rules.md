# Visual Checkpoint Rules

## Purpose

A review cycle is not a full dashboard. It is a focused evidence panel that supports one judgment question.

Every cycle should fit on a single screen together with the multiple-choice and free-text questions.

## Screen-fit rule

Each review cycle must include:

- 2 to 3 metric cards.
- Plus one compact chart or one compact table.
- Plus 3 short evidence bullets.
- Plus one multiple-choice question via the question tool.
- Plus one free-text context capture via the question tool.

Avoid showing both a large table and a chart in the same review cycle. If both are needed, choose the one that best illustrates the question and mention the other in one evidence bullet. The chart-or-table element is mandatory. Cards alone are not sufficient.

## Choose the visual based on the question

### Trend break

Use:

- Line chart.
- Sparkline table.
- Small multiples for closely related metrics.

Show:

- Prior months if available.
- Current month highlighted.
- Budget, forecast, or prior year only if useful.

Do not use:

- A single variance table when the question is about trend.

### Variance explanation

Use:

- Bullet-style bars.
- Variance table.
- Bridge or waterfall.

Show:

- Actual.
- Comparison.
- Variance.
- Materiality label.

Do not color every variance. Highlight only material exceptions.

### Revenue, value driver, or mix quality

Use:

- Contribution table.
- Channel, category, segment, region, product, or customer table.
- Simple stacked or grouped bars only if readable.
- Top driver cards.

Show:

- Share of total.
- Change vs comparison.
- Contribution to growth or variance.

Do not use pie charts or donut charts.

### Margin and profit conversion

Use:

- Bridge chart.
- Margin bps card.
- Profit conversion table.

Show:

- Revenue or activity effect.
- Margin rate effect.
- Opex effect.
- Net profit variance.

### Cash and working capital

Use:

- Cash bridge.
- Working capital movement table.
- Compact risk card.

Show:

- Cash change.
- Key working capital movements.
- Cash vs profit divergence if material.

## Style principles

Use a Stephen Few-inspired style without turning the skill into a design textbook:

- Maximize data-ink ratio.
- Remove decoration that does not help comprehension.
- Use exception highlighting only for true signals.
- Keep most visuals neutral.
- Use preattentive emphasis sparingly.
- Prefer labels near data instead of legends.
- Avoid redundant encoding.
- Avoid 3D, gradients, gauges, pie charts, donuts, and decorative icons.
- Use aligned tables and consistent number formatting.

## Card format

Each card should have:

- Metric label.
- Actual value.
- Comparison value.
- Variance.
- Signal label.

Example:

```text
Revenue
$12.4M
+$0.8M vs budget | +6.9%
Signal: material favorable variance
```

## Table format

Keep tables compact:

- 4 to 6 rows when possible.
- 4 to 6 columns maximum.
- Sort by contribution or materiality.
- Use aligned numeric columns.
- Use bracketed unfavorable variances.
- Do not show unnecessary decimals.

## Chart format

Charts should have:

- Clear title.
- Direct labels or minimal legend.
- Neutral baseline.
- One accent for the material signal.
- Clear units.
- No decorative effects.

## Evidence bullets

After the visual, include exactly 3 short bullets:

1. Confirmed fact.
2. Possible interpretation.
3. What remains uncertain.

Do not add a long narrative before the question.


## Hard minimum composition rule

A review cycle is invalid unless it contains all of the following, visibly in the chat output before the question tool appears:

- 2 to 3 cards
- 1 compact chart or 1 compact table
- 3 short evidence bullets

If space is tight, shrink the chart or the table. Do not drop it.
