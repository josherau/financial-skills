# Koen Advisors Sample Finance Data Pack — May 2026

**Company:** Born2Cycle, Inc. — omnichannel bicycle retailer (Pacific Northwest)
**Reporting currency:** USD
**Period:** May 2026 (Monthly Financial Review)

---

## Situation

Born2Cycle has just closed its May 2026 books and is preparing the monthly financial review for the board.

- Net sales came in **ahead of budget** (+6.4%, $7.40M vs $6.95M).
- Gross margin was **close to budget** (41.6% vs 42.0%).
- EBITDA was **broadly in line with plan** ($250K vs $275K budget).

However, **cash ended the month materially below the cash forecast** — ending cash was **$0.67M against a
forecast of ~$1.70M** — and the company drew **$250K on its revolver** during the month.

The CEO believes the finance team's cash forecast has been too conservative. The board wants a clear
explanation of the cash position before approving the next phase of the Spokane store expansion.

---

## Your task

> You are acting as a CFO investigation agent. You have been given a full May 2026 finance data pack for
> Born2Cycle. Revenue and EBITDA look acceptable, but cash is materially worse than forecast. Investigate
> the data pack and explain why. Do not only summarize the files. Find contradictions, weak signals, stale
> assumptions, working-capital drivers, classification issues, and board narrative risks. Produce a
> CFO-ready memo with quantified root causes, evidence by file, confidence levels, recommended actions, and
> questions for follow-up.

---

## Files in this pack

| # | File | Contents |
|---|------|----------|
| 00 | `00_MODEL_INSTRUCTIONS.md` | This file |
| 01 | `01_pnl_actual_vs_budget_may_2026.csv` | P&L by channel: actual vs budget, prior month, prior year |
| 02 | `02_balance_sheet_apr_may_2026.csv` | Balance sheet, Apr 30 vs May 31, with movement |
| 03 | `03_cash_forecast_vs_actual_13_week.csv` | 13-week cash forecast vs actual, with the assumptions used |
| 04 | `04_ar_aging_detail.csv` | Accounts receivable aging detail |
| 05 | `05_ap_aging_detail.csv` | Accounts payable aging detail |
| 06 | `06_bank_transactions_may_2026.csv` | Bank transactions for May |
| 07 | `07_sales_orders_may_2026.csv` | Sales orders, with expected vs actual cash dates |
| 08 | `08_sales_by_channel_and_store.csv` | Net sales, margin and cash collected by store × channel |
| 09 | `09_customer_master.csv` | Customer master, incl. default and prior payment terms |
| 10 | `10_vendor_master.csv` | Vendor master, incl. payment terms and early-payment discounts |
| 11 | `11_inventory_purchases_and_receipts.csv` | Purchase orders, receipts, expected vs actual sell-through |
| 12 | `12_refunds_returns_chargebacks.csv` | Returns, refunds and chargebacks |
| 13 | `13_payment_processor_settlements.csv` | Stripe / Shopify / Amazon / Walmart / Backcountry settlements |
| 14 | `14_board_pack_draft_comments.md` | Draft CFO board commentary (to review critically) |

**Shared keys** are consistent across files: `customer_id`, `vendor_id`, `store`, `channel`,
`product_category`, and the various id fields (`sales_order_id`, `invoice_id`, `po_id`, `bank_reference`).
Amounts are in whole USD. Figures tie directionally; this is a realistic monthly close, not a penny-perfect
reconciliation.

**Channels:** In-store · Online Direct · Marketplace · Corporate / B2B · Service & Repairs · Warranty Plans
**Stores:** Portland · Eugene · Seattle · Spokane · Bend · Tacoma
**Product categories:** Bikes · E-bikes · Parts · Accessories · Apparel · Service · Warranty
