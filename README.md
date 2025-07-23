# **Trade Recommendation Backtesting System**

## **Introduction**

This project aims to implement a **backtesting system for trade recommendation strategies**, with a strong focus on **order execution logic** and **risk management parameters**. The system is designed to evaluate the historical performance of structured trade recommendations by simulating their execution using past market data.

Each recommendation is composed of a rich set of parameters, closely resembling real-world trading instructions, including order types (e.g., **limit**, **market**, **stop**, and **stop-limit orders**) and risk controls (e.g., **stop-loss**, **trailing-stop**, **hold**, and **take-profit** mechanisms).

The recommendations are structured with the following key fields:

**Core Fields**

- **Date:** timestamp of the recommendation
- **Name:** company name of the traded stock
- **Equity:** the stock or asset ticker under consideration
- **Scenario:** a description of the market or strategy context, the recommendation rationale

**Entry Orders:** entry orders define how and at what price a position is opened

- **Market Order:**
    - indicates immediate execution at current market price
    - since my system operates with daily prices, market orders are executed using the recommendation day's mid-price (which is defined as the average of the high and low prices)
- **Limit Order:**
    - specifies a desired entry price at which the trade should be filled
    - this can be above or below the current price, depending on the recommendation's intention (to buy on a pullback near support or breakout above resistance)
    - if the limit price is reached outside of regular trading hours (during pre-market trading or a gap at the open), the order is filled with the open price
    - until filled, the order remains active and may be modified

**Sell-Limit Orders:** sell-limit orders define profit-taking targets; they are, by definition, placed above the entry price (for long positions); in my system, such targets (exit orders) can be defined using any of the following formats:

- **Sell-Limit Order Percentage:** trigger level expressed as a percentage above the entry price
- **Sell-Limit Order Difference:** absolute currency-based offset from the entry price
- **Sell-Limit Order Exact:** a fixed stop price

**Stop or Stop-Loss Orders:** stop-loss orders (often just called "stops") are used to mitigate potential losses or to protect unrealised gains; depending on trade management, the stop level may be set below or above the entry price; in my system, stop-loss orders can be defined using the following formats:

- **Stop-Loss Order Percentage:** risk level defined as a percentage from the entry price
- **Stop-Loss Order Difference:** absolute currency-based stop from entry price
- **Stop-Loss Order Exact:** a fixed price level at which the position is exited to limit loss

**Trailing-Stop Orders:** trailing stop is a dynamic stop-loss that moves in the favourable direction only; in the case of a long position, the stop price trails behind rising prices, locking in profits while allowing further upside; in my system, trailing stops can be defined using the following formats:

- **Trailing-Stop Order Percentage:** the trailing distance is maintained as a fixed percentage below the peak price
- **Trailing-Stop Order Difference:** a pecific trailing value in absolute currency-based terms that follows price movement, maintaining a fixed distance

**Direct Commands:** these are immediate actions applied to the position, unless stated otherwise

- **Hold:** indicates a recommendation to maintain the position without any changes; during the holding period, no stop orders are activated
- **Close:** signals the immediate closing of an open position, thereby realizing current profit or loss

## **Flowchart**

For the system, I created a flowchart. This shows my logical thinking about orders and their execution.

<img width="4137" height="8445" alt="flowchart" src="https://github.com/user-attachments/assets/a7573345-d01e-45f5-9c85-4eb5256e574c" />


**It is important to note, that the system does not:**
- support short selling or short positions, as it operates only long positions
- account for taxes, fees, or transaction costs associated with trading
- specify position sizes, as it operates with a single position at a time
- account for slippage, assuming that orders are filled at the specified prices
- consider dividends, interest, or other corporate actions
- handle multiple positions or complex order types, focusing on single-entry and single-exit scenarios
- support partial fills, assuming that orders are either fully executed or not executed at all
- open and close positions on the same day, as it operates with daily prices

## **Data**

**Tables and columns**

- `data_equites`: contains data tables of selected equities, named after the stock's ticker, with the following columns:

    - `date`: day of trading prices (timestamp for each trading day)
    - `open`: opening price of the equity for the trading day
    - `high`: highest price reached by the equity during the trading day
    - `low`: lowest price reached by the equity during the trading day
    - `close`: closing price of the equity for the trading day

- `data_orders`:

    - `date`: day of trade recommendation
    - `company`: name of the company for which the recommendation is made
    - `ticker`: ticker symbol of the equity
    - `scenario`: description or rationale for the trade recommendation
    - `buy_market`: indicator (1 or 0) for a market buy order
    - `buy_limit`: price for a limit buy order (buy only if price reaches this value)
    - `sell_limit_pct`: take-profit trigger as a percentage above the entry price
    - `sell_limit_dff`: take-profit trigger as an absolute value above the entry price
    - `sell_limit_xct`: take-profit trigger as an exact price
    - `sell_loss_pct`: stop-loss trigger as a percentage below the entry price
    - `sell_loss_dff`: stop-loss trigger as an absolute value below the entry price
    - `sell_loss_xct`: stop-loss trigger as an exact price
    - `sell_loss_trail_pct`: trailing stop-loss as a percentage below the highest price since entry
    - `sell_loss_trail_dff`: trailing stop-loss as an absolute value below the highest price since entry
    - `hold`: indicator to hold the position (no exit orders active)
    - `sell_market`: indicator for a market sell order (close position at current market price)

- `data_trading`:

    - all columns from `data_equites` and `data_orders`
    - `buy_price`: the price at which a buy order is executed (either market or limit)
    - `sell_price`: the price at which a sell order is executed (market, limit, or stop)
    - `sell_above`: the current active take-profit (sell-limit) price
    - `sell_below`: the current active stop-loss or trailing-stop price,
    - `trade_active`: boolean flag indicating whether a position is currently open (True) or not (False)
    - `trade_price`: the price at which the current trade was opened, and closed
    - `high_so_far`: the highest price reached since the trailing stop was ordered

## **Recommendations**

The recommendations are stored in an excel file, easy to edit and widely understood.

<img width="1643" height="483" alt="recommendations" src="https://github.com/user-attachments/assets/0028bc48-11ba-466e-80f4-4adbe758441a" />


## **Figures**

<img width="998" height="497" alt="TRBS_MSFT" src="https://github.com/user-attachments/assets/7bd48ae4-936a-4b43-8725-53f37df15bce" />
<img width="1004" height="499" alt="TRBS_NFLX" src="https://github.com/user-attachments/assets/d58445cb-9604-423a-ab27-8896b768430a" />
<img width="997" height="496" alt="TRBS_DIS" src="https://github.com/user-attachments/assets/24e5ae62-eb89-4be2-bb4c-68601ca4efb5" />
<img width="998" height="496" alt="TRBS_AMZN" src="https://github.com/user-attachments/assets/2c45a3b5-99a9-444c-bd51-ead7e5fc3c3d" />
<img width="998" height="496" alt="TRBS_META" src="https://github.com/user-attachments/assets/bbdb9804-1e18-4324-950a-a11d2d117fb4" />
<img width="999" height="500" alt="TRBS_TSLA" src="https://github.com/user-attachments/assets/7543fbe2-8f73-4d5c-80b3-2f589bb97fc5" />



