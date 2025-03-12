# Small Case Performance

## Performance Calculation

### Assumption: Static Composition Throughout the Year
The performance of the small case is calculated under the assumption that the composition of assets remains unchanged throughout the entire year. This means that the portfolio allocation at the beginning of the period is maintained across all historical data points, using the current day's composition as a reference for the past year's performance.

## Methodology

### One-Time Investment Assumption
We assume that a one-time investment is made into a crypto bundle. This bundle consists of a specific set of cryptocurrencies, each with a defined allocation percentage. The investment is then tracked over time to measure its returns.

### Backfilling Performance Data
1. **Historical Performance Calculation**: 
   - To provide historical performance data, we backfill the past one year’s performance using the current asset allocation.
   - This means that we assume that if the same assets with the same allocations had existed for the past year, they would have yielded the same returns as calculated retrospectively.
   - Example: If the current allocation consists of 40% Bitcoin, 30% Ethereum, and 30% Solana, we apply this allocation retroactively to historical price data to simulate past performance.
   
2. **Daily Performance Tracking via Cron Job**:
   - A scheduled cron job is set up to record the portfolio’s performance daily.
   - This cron job ensures that the latest composition on any given day is considered for calculating returns from that day onward.
   - Example: If on January 1st, the portfolio composition was 50% Bitcoin, 30% Ethereum, and 20% Solana, and on February 1st, it changed to 40% Bitcoin, 40% Ethereum, and 20% Solana, then from February 1st onward, calculations will be based on the updated allocations.

### Rebalancing and Investment Amount Adjustment
- **Tracking Latest Case-Invested Value**:
   - Whenever a rebalance occurred, we tracked the latest case-invested value, which changes over time.
   - Instead of using the initial investment amount, the newly adjusted investment value was redistributed based on the latest allocations.
   - This ensures that the investment amount remains steady, effectively allowing the initial investment to "roam around" within the portfolio while adapting to changes in allocations.
   
- **Example of Rebalancing and Reinvestment**:
   - Suppose an investor starts with $10,000 in a crypto bundle allocated as:
     - 50% Bitcoin ($5,000)
     - 30% Ethereum ($3,000)
     - 20% Solana ($2,000)
   - Over time, due to price changes, the total portfolio value grows to $12,000, with uneven distribution:
     - Bitcoin: $6,500
     - Ethereum: $3,200
     - Solana: $2,300
   - During the next rebalance, instead of using the original $10,000 investment, the system redistributes the current portfolio value of $12,000 according to the latest allocation weights.

### Performance Calculation Logic
- **Historical Returns:** Using the latest available asset composition, we simulate past performance by applying historical price movements to the assumed allocations.
- **Daily Updates:** As the portfolio composition updates over time, daily performance is computed based on the updated allocations, ensuring that the performance data reflects real-world changes.

## Why This Approach?
- **Consistency in Measurement:** Using a fixed allocation for backfilling ensures that comparisons between past and present performance are meaningful.
- **Realistic Performance Tracking:** By incorporating daily updates from a cron job, we align the performance calculations with actual market movements and rebalancing strategies.
- **Adaptive Investment Allocation:** By redistributing the case-invested value instead of the initial investment, the investment adapts dynamically to market changes while maintaining its original intent.
- **Simplified User Experience:** Investors can view historical performance seamlessly without worrying about changing allocations skewing past returns.
- **Better Portfolio Management:** Investors benefit from an automatically adjusting investment strategy that maintains alignment with current market conditions while preserving past performance records.

## Summary
This method of performance calculation allows for a clear and structured evaluation of a small case’s returns. By backfilling performance with a fixed allocation and updating daily via a cron job, the portfolio performance remains transparent and easy to track for investors. The approach of tracking the latest case-invested value ensures that the investment amount remains fluid and adjusts over time, providing a realistic representation of portfolio growth and performance. With rebalancing ensuring that the latest investment value is redistributed rather than the initial capital, the approach mimics a real-world scenario where capital dynamically moves within the portfolio while maintaining a steady investment footprint.
