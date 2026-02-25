[🏠 Document Start](../README.md) / [Trading Operations](README.md) / Depth of Market

[Previous](Basic-Principles.md) | [Next](Market-Watch.md)

<a id="depth-of-market"></a>
# Depth of Market (#depth-of-market)

The Depth of Market (DOM) displays bids and asks for a particular instrument at the currently best prices (closest to the market).

The Dept of Market is different on the exchange and over-the-counter markets:

  * If an instrument is traded in the exchange mode, in which related trading operations are sent to an external trading system (an exchange), the DOM features real prices and order volumes from market participants.
  * If an instrument is traded in the over-the-counter (OTC) market, the Depth of Market can be formed based on the quotes of the broker, who may provide different prices depending on the buy or sell volume. If the broker does not provide volumes, the DOM window functions as a scalping tool, which allows placing of market and pending orders with a single click. In this case, the Depth of Market displays price levels calculated based on the Bid and Ask prices using the price change step.



For more information about prices in the Depth of Market, please see the [Price Data](For-Advanced-Users/Price-Data.md) section.

![The depth of market displays information on buy and sell orders](images/dom.png)

To open the depth of market of a financial instrument, click "![Depth of Market](images/dom_icon.png) Depth of Market" in the context menu of the [Market Watch](Market-Watch.md).

  * The number of bids and offers displayed in the DOM is determined by the symbol parameters set by the broker.


  * The availability of the Depth of Market feature for exchange instruments is not guaranteed and depends on your broker.

  
---  
  
Operations of two types are performed from the depth of market:

  * Market Operations — buying/selling a financial instrument at the current market price;
  * Trade Requests — placing various trade requests ([pending orders (#pending-order)](Basic-Principles.md#pending-order)) to buy/sell a financial instrument at a specified price (which is currently unavailable on the market).



<a id="market"></a>
## Market Operations (#market)

A market operation is buying/selling a financial instrument at the best price currently offered in the market.

Execute a market operation from the depth of market. Click on the appropriate trade command in the depth of market of the appropriate [symbol](Market-Watch.md) specifying the required amount. If ["One Click Trading" (#one-click)](../Getting-Started/Platform-Settings.md#one-click) is enabled, this request is immediately sent to the server without specifying any extra conditions (trading dialog is not displayed).

Suppose we have executed a 20-lot buy operation, while the following offers are currently available in the market:

![Market offers in the depth of market](images/market_example_dom.png)

Since we have requested 20 lots with the Fill or Kill condition at the market price, the required volume will be made up of the nearest market bids. If the order contained a certain price, then it would be executed only at this specified price and only in the specified volume.

You can view the history of order execution in the ["History" (#trade-history)](Executing-Trades.md#trade-history) tab of the "Toolbox" window:

![The order is filled by several offers closest to the market](images/market_example_history.png)

You see here that the final volume of 20 lots was received from a few offers closest to the market. The corresponding offers disappear from the depth of market.

<a id="request"></a>
## Trade Requests (#request)

Placing a trade requests means creating a [pending order (#pending-order)](Basic-Principles.md#pending-order) to buy/sell a financial instrument at a specified price, which is currently not available on the market. Depending on how requests are processed on the server, they can be displayed directly in depth of market (mostly limit requests) or wait for execution on the broker's side (mostly stop or stop limit requests) and then be converted into a market order.

Here is an example of placing a limit request to buy 3 lots of the futures contract RTS-6.13. Specify the required volume in the "vol" field and click on ![Set Buy Limit](images/dom_buy_limit_button.png) (in the Bid price area for the Buy Limit order) or ![Set Sell Limit](images/dom_sell_limit_button.png) (in the Ask price area for the Sell Limit order) in the "Trade" column in the line of the price, at which you wish to place an order. If ["One Click Trading" (#one-click)](../Getting-Started/Platform-Settings.md#one-click) is enabled, this request is immediately sent to the server without specifying any extra conditions (trading dialog is not displayed).

> Examine "Quick trading" section to learn how to quickly manage orders in the depth of market.

When placed successfully, the request appears in the depth of market:

![The placed request is displayed in DOM](images/pending_dom_example.png)

The newly placed order is displayed in the "Trade" column — BLIM 3 (Buy Limit order of 3 lots). As soon as there is a market participant ready to sell the financial instrument at the specified price, the order will be filled and will turn into a position.

<a id="stop-and-stop-limit-orders"></a>
### Stop and Stop Limit Orders (#stop-and-stop-limit-orders)

Usually, [Stop and Stop Limit Orders (#pending-order)](Basic-Principles.md#pending-order) (Buy Stop, Sell Stop, Buy Stop Limit and Sell Stop Limit) are not sent to an external trading system (exchange) directly as opposed to limit orders. Until reaching the [stop price (#pending-place)](Executing-Trades.md#pending-place), these orders are processed within the MetaTrader 5 platform.

  * Upon reaching the stop price specified in a Buy Stop or Sell Stop order, an appropriate market operation is executed.
  * Upon reaching the stop price specified in a Buy Stop Limit or Sell Stop Limit order, an appropriate limit request is executed, which will be visible to other market participants.



<a id="quick-trading"></a>
## Quick Trading from the Depth of Market (#quick-trading)

The depth of market allows users to quickly manage stop levels (Stop Loss and Take Profit) and pending orders of open positions. This option is only available with the ["One Click Trading" (#one-click)](../Getting-Started/Platform-Settings.md#one-click) option enabled in the trading platform settings. Trade requests are sent from the depth of market instantly without showing a trading dialog.

<a id="moving-stop-levels"></a>
### Moving Stop Levels (#moving-stop-levels)

Stop levels of open positions are displayed in the "Trade" column as TP (Take Profit) and SL (Stop Loss). These levels can be moved by mouse:

![To modify a stop level, drag it in the depth of market](images/dom_stops_move.png)

Move a level to the line with the required price, and it will be modified instantly.

<a id="deleting-stop-levels"></a>
### Deleting Stop Levels (#deleting-stop-levels)

Stop levels can be deleted from Depth of Market:

![To remove a stop level, place the cursor on it and press X](images/dom_stops_delete.png)

Hover the mouse cursor over the button ![Set Sell Limit/Sell Stop](images/dom_sell_limit_button_1.png) (or ![Set Buy Limit/Buy Stop](images/dom_buy_limit_button_1.png)) to the right or to the left from the level and click Shift. The button will change its view to ![Delete level](images/dom_order_delete_button.png). Click the button to delete the level.

<a id="pending-place"></a>
### Placing Orders (#pending-place)

[Pending orders (#pending-order)](Basic-Principles.md#pending-order) are placed using buttons ![Set Buy Limit/Buy Stop](images/dom_buy_limit_button_2.png) or ![Set Sell Limit/Sell Stop](images/dom_sell_limit_button_2.png) next to the desired price:

  * To place a Buy Limit order, click ![Set Buy Limit](images/dom_buy_limit_button_3.png) in the Bid price area.
  * To place a Buy Stop order, click ![Set Buy Stop](images/dom_buy_limit_button_4.png) in the Ask price area.
  * To place a Sell Limit order, click ![Set Sell Limit](images/dom_sell_limit_button_3.png) in the Ask price area.
  * To place a Sell Stop order, click ![Set Sell Stop](images/dom_sell_limit_button_4.png) in the Bid price area.



![To place a limit order, click the up or down arrow at the required level](images/dom_pending_place.png)

After that, an order is placed at the specified price. It has the volume set in the "vol" field, as well as Stop Loss and Take Profit levels specified in "sl" and "tp" fields, respectively.

<a id="modification-of-orders"></a>
### Modification of Orders (#modification-of-orders)

The depth of market allows users to easily change prices of previously set orders.

![To modify a limit order, drag it to a new level](images/dom_pending_move.png)

Move the pending order to the necessary price line. The order price changes instantly. If the Stop Loss and Take Profit levels are set for the order, they are moved by the same distance as the price.

If we drag a limit order through the ask/bid border, it will change to a stop order (Buy Limit will be replaced by Buy Stop, while Sell Limit - by Sell Stop).

![To change the order type, drag it across the border of buy and sell offers](images/dom_pending_change_type.png)

> If several same price orders are placed, they cannot be moved in the depth of market.

<a id="deleting-orders"></a>
### Deleting Orders (#deleting-orders)

To delete an order from the depth of market, hover the mouse cursor over ![Set Sell Limit/Sell Stop](images/dom_sell_limit_button_5.png) (or ![Set Buy Limit/Buy Stop](images/dom_buy_limit_button_5.png)) to the right and click Shift. The button will change its view to ![Delete level](images/dom_order_delete_button_1.png). Click the button to delete the order.

![To remove a pending order, place the cursor on it and press X](images/dom_pending_delete.png)

> If several same price orders are placed, the oldest one is removed first.

<a id="timesales"></a>
## Time & Sales and Tick Chart (#timesales)

Time and sales and a tick chart of exchange instruments with real transaction prices is displayed in the Depth of Market.

<a id="time-sales"></a>
### Time & Sales (#time-sales)

The Time & Sales feature provides the price and time of every trade executed on the exchange. Information on every trade includes the time when the trade was executed, its direction (buying or selling), as well as the price and volume of the trade. For easy visual analysis, different colors are used to indicate different trade directions: blue is used for Buy trades, pink for Sell trades, green means undefined direction. Trade volumes are additionally displayed in a histogram.

![Time & Sales](images/time_and_sales.png)

How Time & Sales can help you understand the market

The Time & Sales feature provides tools for a more detailed market analysis. The trade direction suggests who has initiated the trade: the buyer or the seller. The volume of trades allows traders to understand the behavior of market participants: whether the trades are performed by large or small market players, as well as estimate the activity of the players. The trade execution speed and the volume of trades on various price levels help traders to estimate the importance of the levels.

How to use Time & Sales data

In addition to the visual analysis of the table, you can save the details of trades to a CSV file. Further, they can be analyzed using any other software, such as MS Excel. The file contains comma-separated data:

Time,Bid,Ask,Last,Volume,Type  
2016.07.06 16:05:04.305,89360,89370,89370,4,Buy  
2016.07.06 16:05:04.422,89360,89370,89370,2,Buy  
2016.07.06 16:05:04.422,89360,89370,89370,10,Buy  
2016.07.06 16:05:04.669,89360,89370,89370,1,Buy  
2016.07.06 16:05:05.968,89360,89370,89360,7,Sell  
---  
  
If you want to save data to a file, open the context menu and select "Export Ticks to CSV".

Filter by Volume

Deals with the volume less than the specified value can be hidden from the Time & Sales table. This filter allows to show only large deals in the Time & Sales window.

Double click on the first line in the Time & Sales window, specify the minimum volume in lots, and then click on any other area of ​​the Market Depth. Trades will be filtered, and the current filter value will appear in the volume column header.

![Filtering trades by volume](images/time_sales_filter.png)

You can also specify the minimum volume using the Time & Sales context menu.

<a id="tick-chart"></a>
### Tick Chart (#tick-chart)

All transactions conducted on the Exchange are plotted on this chart:

  * Red circles show Sell transactions.
  * Blue circles show Buy transactions
  * Green circles appear when the direction of the transaction is undefined. It is used when the exchange does not transmit the direction of a transaction. In this case, the direction is determined based on the price of the transaction as compared to prices bid and ask. A Buy transaction is that executed at the ask price or above, a Sell transaction is executed at the bid price or lower. The direction is undefined if the price of the transaction is between the bid and the ask.



![A tick chart with Time & Sales](images/dom_1.png)

The larger the circle, the greater the volume of the transaction. Transaction volumes are also shown as a histogram below the tick chart.

Using the "Synchronize" command in the context menu, you can control the display of deals charts (circles and histogram):

  * In the synchronous mode, the deals chart is tied to the tick chart and they both have the same time scale.
  * In the independent mode, the deals chart is not tied to the tick chart, and the deals are drawn one by one.



At the top and bottom of the histogram, the total volumes of the current Buy and Sell offers are shown.

> The vertical scale of the tick chart is the Market Depth (i.e. its levels). Price change ranges which are not available in market depth are displayed as straight lines on the tick chart. To view the most accurate tick chart, enable the extended mode and the display of spread values for the Market Depth.

<a id="toolbar"></a>
## Toolbar (#toolbar)

To customize the appearance of the depth of market, use the toolbar at the top of the window:

  * ![Show/hide the tick chart.](images/dom_tick_chart_icon.png) — show/hide the tick chart.
  * ![Show/hide Time & Sales](images/time_and_sales_icon.png) — show/hide Time & Sales.
  * ![Bind the Market Depth to an active chart](images/dom_link_icon.png) — binding the Market Depth to an active chart. Every time you switch to a chart of a financial instrument, the same instrument will be automatically enabled in the Market Depth window. So, you will not need to open the Market Depth window for each new symbol.
  * ![Switch to the advanced mode](images/dom_advanced_icon.png) — switch to the advanced mode; every step of the price will be displayed in the depth of market, regardless of whether there are any offers at this price.
  * ![Show spread in the DOM](images/dom_spread_icon.png) — show the spread in the depth of market.
  * ![Show/hide Bid and Ask charts](images/dom_bidask_icon.png) — show/hide the Bid and Ask price charts.
  * ![Show/hide trades](images/dom_timesales_icon.png) — show/hide transactions that appear in the form of circles on the tick chart.
  * ![Zoom in the chart](images/dom_zoomin_icon.png) — zoom in the chart.
  * ![Zoom out the chart](images/dom_zoomout_icon.png) — zoom out the chart.



Most of these commands are also available in the context menu of the Market Depth and Time & Sales windows. The context menu of the scalping Depth of Market (for non-exchange instruments) also allows switching between the volume in lots and units.
