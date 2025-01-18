
# **Trading Orders - Learning and Visualising**
The best way of learning is by doing. To learn the trading order basics, I am going to write this script and watch closely, how stock market works when placing different order types. As I am a visual learner, most of the steps will be plotted on figures. The emphasis is on the order types and their execution, while experimenting python codes and libraries.

## **What is a Trade Order?**
An order is an instruction to buy or sell on a trading venue such as a stock market, bond market, commodity market, financial derivative market or cryptocurrency exchange. These instructions can be simple or complicated, and can be sent to either a broker or directly to a trading venue via direct market access.
 
There are some standard instructions for such orders. Two of the most basic stock order types are **market orders** and **limit orders**, but there are several other types such as, **time in force**, **conditional orders**, etc.


## **Market Order**

A market order is the most basic type of trade. It's an order to buy or sell it immediately at the next price available. Typically, if you buy a stock, you will pay a price at or near the posted ask. If you're going to sell a stock, you will receive a price at or near the posted bid you see on your screen.

One important thing to remember is that the last traded price is not necessarily the one your market order will get. In fast-moving and volatile markets, prices change fast, and your investment strategies need to account for the cost changing a bit from what was last posted on the screen. The price will remain the same only when the bid/ask price is exactly at the last traded price.

*Market orders do not guarantee a price, but they do guarantee the order is filled immediately.*

**Example:** only the purchasing/selling amount and the exact time is given
- Buying 2 shares at 2024-06-11 12:30
- Selling 1 share at 2024-07-23 10:30
- Buying 1 share at 2024-10-23 15:30
- Selling 2 shares at 2024-11-29 11:30

![marketorder](https://github.com/user-attachments/assets/43055556-8162-4458-98f3-cc4cf603f23d)


## **Limit Order**

A limit order, sometimes referred to as a pending order, allows investors to buy and sell securities at a certain price in the future. This type of order is used to execute a trade if the price reaches the preset level; the order will not be filled if the price does not reach this level. In effect, a limit order sets the maximum or minimum price at which you are willing to buy or sell.

A *buy limit* order can only be executed at the limit price or lower.
A *sell limit* order is analogous; it can only be executed at the limit price or higher.

**Example:** only the limits are given (for the sake of simplicity, only one for the whole period)

- Buy limit: $415 or lower
- Sell limit: $435 or higher

![limitorder](https://github.com/user-attachments/assets/c8ad408c-9346-45cf-9a47-9d2b67a01086)
