# Bundle Returns Calculation Using Delta Market Cap Model

## Overview
This model calculates bundle returns based on the **delta in market capitalization (mcap)** of the assets within the bundle. The objective is to dynamically adjust allocations each month based on changes in market capitalization while also simulating hypothetical investments made on a systematic monthly basis (SIP approach). This ensures a fair and logical performance tracking mechanism that accurately reflects real-world market movements.

## Methodology

### Step 1: Initial Investment Setup (One Year Ago)
- The investment simulation starts exactly **one year ago** using the **current bundle composition**.
- On that date, we assume an initial equal distribution across all coins in the bundle.
- The first month’s allocation is calculated as:
  
  **Initial Weight per Coin = 100% / Total Coins in Bundle**
  
#### Example:
If the bundle contains **5 coins**, each coin starts with:
  
  **Weight = 100% / 5 = 20% each**
  
### Step 2: Month-on-Month Allocation Adjustments Using Delta Mcap
From the second month onward, we adjust allocations based on:
1. **Previous month’s market capitalization (prevMcap)**
2. **Current month’s market capitalization (currentMcap)**
3. **Previous month’s allocation weight (prevWeight)**

The new allocation for each coin is calculated as:
  
  **New Allocation = prevWeight × (currentMcap / prevMcap)**
  
After calculating the new allocation for all coins, we normalize them to ensure the total allocation sums up to 100%.

#### Example:
Consider a bundle with **3 coins (BTC, ETH, SOL)** and initial equal allocations:
- Month 1: BTC (33.33%), ETH (33.33%), SOL (33.33%)
- Month 2 Mcap Changes:
  - BTC: **Increased by 10%**
  - ETH: **Decreased by 5%**
  - SOL: **Increased by 20%**
- New Allocation Calculation:
  - BTC = **(33.33%) × (1.1) = 36.66%**
  - ETH = **(33.33%) × (0.95) = 31.66%**
  - SOL = **(33.33%) × (1.2) = 39.99%**
- Normalize allocations:
  - BTC = **34.48%**, ETH = **29.78%**, SOL = **35.74%**

This process continues each month, ensuring that allocations are adjusted dynamically based on market trends.

### Step 3: Systematic Investment Plan (SIP) Simulation
- In addition to tracking a one-time investment made **one year ago**, we also simulate hypothetical **monthly investments** on the **same date of each month**.
- This helps in calculating SIP-based portfolio performance, reflecting a more systematic approach to investing.
- Each monthly investment is allocated based on the **latest composition weights** determined through the delta mcap model.

#### Example:
- If an investor **starts investing $1,000 per month**, then:
  - Month 1: $1,000 invested as per equal weights.
  - Month 2: $1,000 invested using adjusted delta-mcap weights.
  - Month 3: $1,000 invested again, but using the new updated allocations.
- Over **12 months**, the total investment will be **$12,000**, but each installment would have been distributed dynamically across assets based on the latest market cap changes.

### Step 4: Portfolio Value Calculation
For each month:
1. **Investment Amount** = Amount invested in that month
2. **Portfolio Value** = Sum of the latest value of all holdings based on market prices
3. **Returns Calculation**:
   
   **Returns = (Portfolio Value - Total Investment) / Total Investment × 100%**

### Step 5: Daily Data Points for Performance Tracking
- The same model is extended to **daily intervals** to provide granular data points.
- This helps in constructing an **accurate performance graph** by tracking the market fluctuations on a finer scale.

## Why This Approach?
- **Realistic Portfolio Adjustments**: Instead of static allocations, weights adjust dynamically based on market capitalization changes.
- **Better Performance Tracking**: Ensures month-on-month adjustments capture real-world market conditions.
- **SIP & One-Time Investment Models**: Supports both lump sum and systematic investing strategies for a broader investment analysis.
- **Accurate Graph Representation**: Daily tracking allows for a detailed performance visualization, enhancing decision-making for investors.

## Summary
This delta-mcap-based model calculates portfolio performance by:
1. **Starting with equal allocations one year ago**
2. **Adjusting monthly allocations based on market capitalization changes**
3. **Simulating SIP investments for systematic performance tracking**
4. **Calculating portfolio value and returns dynamically**
5. **Providing daily performance tracking for accurate graph visualization**

This approach ensures precise and adaptive portfolio tracking, making it a robust method for investment analysis.
