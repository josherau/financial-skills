# Few-Inspired Dashboard Rules

## Intent

Use these rules to create visual output that is clear, dense, and decision-ready.

This is not a decorative design system. It is a monitoring and management communication system.

## Signal vs noise

- Signal is meaningful variation that warrants attention or action.
- Noise is routine movement that does not warrant attention.

The dashboard must separate signal from noise. Do not color every variance red or green. Most metrics should remain neutral. Only true exceptions get emphasis.

## Preferred visual components

### Bullet-style bars

Use for actual vs target, actual vs budget, actual vs forecast, or current vs threshold.

Rules:

- Use a linear scale starting at zero unless the metric is a variance around zero.
- Actual is the primary bar.
- Budget, forecast, or target is a thin marker.
- Use muted neutral ranges if helpful.
- No 3D, gradients, shadows, or decorative borders.

### Sparklines

Use for compact trends in tables.

Rules:

- Thin line.
- No axes unless the user needs exact reading.
- Same scale for comparable rows.
- Highlight current month only when relevant.

### Exception indicators

Use small red or amber markers only for material exceptions.

Rules:

- Red means material downside or urgent risk.
- Amber means watch item.
- No indicator means normal or not material.
- Do not create traffic-light dashboards where every row gets a color.

### Bridges

Use for profit conversion, cash movement, and variance explanation.

Rules:

- Start with the comparison baseline.
- Show the few largest drivers.
- End with actual.
- Group small residual items as "Other" if needed.

### Tables

Use for detailed but compact management views.

Rules:

- Sort by materiality or contribution.
- Align numbers right.
- Use clear units.
- Use bracketed unfavorable variances.
- Minimize borders and heavy gridlines.
- Avoid dense raw data dumps.

## Chart selection

| Relationship | Preferred visual |
|---|---|
| Time series | Line chart or sparkline |
| Ranking | Horizontal bar chart |
| Part-to-whole | Stacked bar or contribution table |
| Deviation | Variance table, bullet bar, or bridge |
| Distribution | Histogram or strip plot when useful |
| Correlation | Scatter plot when useful |
| Nominal comparison | Horizontal bar chart or compact table |

Never use pie charts, donut charts, gauges, radar charts, 3D charts, decorative icons, or stock images.

## Density rule

The final MFR deck should feel like a CFO dashboard deck, not a marketing presentation. Use enough density to support decision-making, but avoid overwhelming the reader.

Each final slide should include:

- One clear message.
- One primary visual.
- One compact supporting table or card row.
- One management implication.

## Labels and legends

Prefer direct labels near data. Avoid legends when labels can be placed near the marks. If a legend is necessary, keep it short and stable across slides.
