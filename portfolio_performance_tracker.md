# Portfolio Performance

## Overview
The portfolio performance calculation is based on tracking individual user investments, their respective coin compositions, and their performance over time. This process ensures that each user's investment returns are accurately measured and aggregated to provide a complete portfolio view.

## Methodology

### Investment-Based Performance Calculation
- When a user makes an investment, we store:
  - The amount invested
  - The coin composition at the time of investment
  - The quantity of each coin purchased
- This data allows us to track the exact value of the user's holdings over time by comparing it with daily coin prices.

#### Example:
- User invests **$1,000** on **January 1st** into a crypto bundle containing:
  - **50% Bitcoin (BTC) → $500 worth at $50,000 per BTC → 0.01 BTC**
  - **30% Ethereum (ETH) → $300 worth at $2,500 per ETH → 0.12 ETH**
  - **20% Solana (SOL) → $200 worth at $100 per SOL → 2 SOL**
- We store the exact quantities of BTC, ETH, and SOL purchased.
- Every day, we fetch the latest market prices and calculate the current value of these holdings.

### Backfilling Performance Data
- If an investment was made on a past date, we calculate performance retrospectively to ensure complete historical data.
- The system fills in performance data from the investment date until the current date.

#### Example:
- If a user invested on **July 1st**, but performance tracking starts from **August 1st**, we backfill data for the missing month using stored quantities and historical prices.
- This ensures the user sees a full performance history from the actual investment date.

### Daily Performance Calculation via Cron Job
- A scheduled cron job runs daily to:
  - Fetch all investments from the database.
  - Compute each user's investment performance using the latest market prices.
  - Update the performance records accordingly.

#### Example:
- On **March 1st**, market prices change:
  - BTC → **$60,000**
  - ETH → **$3,000**
  - SOL → **$120**
- The user’s portfolio value is recalculated:
  - **0.01 BTC** × **$60,000** = **$600**
  - **0.12 ETH** × **$3,000** = **$360**
  - **2 SOL** × **$120** = **$240**
  - **Total Portfolio Value = $1,200 (20% gain)**
- This new portfolio value is stored and displayed to the user.

## Portfolio Performance Aggregation
- **User Portfolio Performance** is the sum of all individual investment performances under a user's account.
- This aggregation provides a holistic view of how the user's total investments have performed over time.
- Since each investment is tracked with specific quantities of purchased assets, portfolio performance remains accurate and reflects real-time market movements.

#### Example:
- If a user has **three separate investments**:
  - Investment A (BTC, ETH, SOL) → $1,200 value (20% gain)
  - Investment B (ADA, MATIC) → $800 value (-10% loss)
  - Investment C (LTC, AVAX) → $1,500 value (50% gain)
- Portfolio Performance = **$1,200 + $800 + $1,500 = $3,500 total portfolio value**

## Why This Approach?
- **Accurate Historical Performance:** Ensures users have a full record of how their investments have evolved.
- **Daily Updates:** Keeps performance data fresh and reflective of current market conditions.
- **User-Specific Tracking:** Instead of a general index-based performance, we calculate based on real investments made by users.
- **Comprehensive Portfolio View:** Aggregated investment performance offers a single, easy-to-understand metric for users to track their portfolio growth.

## Summary
Portfolio performance is derived from individual investment performances by tracking the user’s purchased coin quantities and comparing them with daily market prices. The system ensures accurate backfilling for historical investments and real-time updates via daily cron jobs, providing users with a transparent and dynamic view of their investment performance. By maintaining granular tracking at the investment level, users can get precise insights into how their portfolio evolves over time, with clear visibility into gains, losses, and overall trends.
