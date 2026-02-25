[🏠 Document Start](../../README.md) / [Trading Operations](../README.md) / [For Advanced Users](../For-Advanced-Users.md) / Margin Calculation: Retail Forex, Futures

[Previous](Price-Data.md) | [Next](Margin-Calculation-Exchange-Model.md)

<a id="margin-calculation-for-retail-forex-futures"></a>
# Margin Calculation for Retail Forex, Futures (#margin-calculation-for-retail-forex-futures)

The trading platform provides different risk management models, which define the type of pre-trade control. The following models are currently available:

  * [For Retail Forex, Futures](Margin-Calculation-Retail-Forex-Futures.md) — used for the OTC market. Margin calculation is based on the type of instrument.
  * [For Stock Exchange, based on margin discount rates](Margin-Calculation-Exchange-Model.md) — used for the exchange market. Margin calculation is based on the discounts for instruments. Discounts are set by the broker, however they cannot be lower than the exchange set values.



The margin is charged for securing traders' open positions and orders.

The first stage of the margin calculation is defining if an account has positions or pending orders for the symbol, for which a trade is performed.

  * If the account has no positions and orders for the symbol, the margin is calculated using the formulas below.
  * If the account has an open position, and an order of any type with the volume being less or equal to the current position is placed in the opposite direction, the total margin is equal to the current position's one. Example: we have a 1 lot EURUSD Buy position and place an order to Sell 1 lot EURUSD (similarly for Sell Limit, Sell Stop and Sell Stop Limit).
  * If the account has an open position, and an order of any type is placed in the same direction, the total margin is equal to the sum of the current position's and placed order's margins.
  * If the account has an open position, and an order of any type with the volume exceeding the current position is placed in the opposite direction, two margin values are calculated - for the current position and for the placed order. The final margin is taken according to the highest of the two calculated values.
  * If the account has two or more oppositely directed market and limit orders, the margin is calculated for each direction (Buy and Sell). The final margin is taken according to the highest of the two calculated values. For all other order types (Stop and Stop Limit), the margin is summed up (charged for each order).



Below are the symbol margin calculation formulas according to their type and settings. The final margin is calculated in three stages:

  * Basic calculation for a certain symbol;
  * [Conversion of the margin currency into the deposit one (#conversion)](Margin-Calculation-Retail-Forex-Futures.md#conversion)
  * [Multiplication by factor (#rate)](Margin-Calculation-Retail-Forex-Futures.md#rate)
  * [Considering trading symbols that are in spread (#spread)](Margin-Calculation-Retail-Forex-Futures.md#spread)
  * [Accounting multiple positions/orders of the same symbol (#hedging)](Margin-Calculation-Retail-Forex-Futures.md#hedging)



<a id="main"></a>
## Basic Calculation for a Symbol (#main)

> If "Initial margin" parameter value is set in the [symbol specification (#specification)](../Market-Watch.md#specification), this value is used. The formulas described in this section are not applied.

The trading platform provides several margin requirement calculation types depending on the financial instrument. Calculation type is displayed in the "Calculation" field of the [symbol specification (#specification)](../Market-Watch.md#specification):

<a id="forex"></a>
### Forex (#forex)

The margin for the Forex instruments is calculated by the following formula:

Volume in lots * Contract size / Leverage

For example, let's calculate the margin requirements for buying one lot of EURUSD, while [the size of one contract (#specification)](../Market-Watch.md#specification) is 100,000 and the leverage is 1:100.

![Margin calculation for Forex symbols](images/margin_forex.png)

After placing the appropriate values to the equation, we will obtain the following result:

1 * 100 000 / 100 = 1 000 EUR

So, now we have the margin requirements value in [base currency (#specification)](../Market-Watch.md#specification) (or [margin currency (#specification)](../Market-Watch.md#specification)) of the symbol.

  * Generally, margin requirements currency and symbol's base currency are the same. If the margin currency is different, calculation results are displayed in that currency instead of the symbol's base one.


  * In this mode, a trader leverage is taken into account even if a [fixed margin (#fixed)](Margin-Calculation-Retail-Forex-Futures.md#fixed) is set.

  
---  
  
<a id="noleverage"></a>
### Forex No Leverage (#noleverage)

This type of calculation is also used for Forex symbols. But unlike the previous one, it does not take into account the trader's leverage:

Volume in lots * Contract size

For example, let's calculate the margin requirements for buying one lot of EURUSD, while [the size of one contract (#specification)](../Market-Watch.md#specification) is 100 000 and the leverage is 1:100. After placing the appropriate values to the equation, we will obtain the following result:

1 * 100,000 = EUR 100,000

So, now we have the margin requirements value in base currency (or margin currency) of the symbol.

> Generally, margin requirements currency and symbol's base currency are the same. If the margin currency is different, calculation results are displayed in that currency instead of the symbol's base one.

<a id="contracts-exchange-stocks"></a>
### Contracts, Exchange Stocks (#contracts-exchange-stocks)

The margin requirements for contracts and stocks are calculated using the following equation:

Volume in lots * Contract size * Open market price

The current market Ask price is used for buy deals, while the current Bid price is used for sell ones.

For example, let's calculate the margin requirements for buying one lot of #AA, the size of the contract is 100 units, the current Ask price is 33.00 USD.

![Margin calculation for Exchange Stocks](images/margin_stocks.png)

After placing the appropriate values to the equation, we will obtain the following result:

1 * 100 * 33.00 = 3300 USD

So, now we have the margin value in base currency (or margin currency) of the symbol.

<a id="contracts-leverage"></a>
### Contracts Leverage (#contracts-leverage)

The leverage is also considered in this type of margin requirement calculation for contracts:

Volume in lots * Contract size * Open market price / Leverage

<a id="contracts-index"></a>
### Contracts Index (#contracts-index)

For index contracts, the margin requirements are calculated according to the following equation:

Volume in lots * Contract size * Open market price * Tick price / Tick size

In this formula, the ratio of [price (#specification)](../Market-Watch.md#specification) and tick [size (#specification)](../Market-Watch.md#specification) is considered in addition to common contracts calculation.

![Margin calculation for CFD Index](images/margin_cfd_index.png)

<a id="futures"></a>
### Futures, Exchange Futures (#futures)

There are two types of the margin requirements for futures contracts:

  * Initial margin is the amount that must be available on the account at the moment of attempting to enter the market. Further maintenance of the same sum may not be obligatory.
  * Maintenance margin is the minimum amount that must be available on the account for maintaining an open position.



Both values are specified in the [symbol specification (#specification)](../Market-Watch.md#specification).

![Margin calculation for Futures and Exchange Futures](images/margin_exchange.png)

The final size of the margin depends on the volume:

Volume in lots * Initial margin

Volume in lots * Maintenance margin

> If the amount of the maintenance margin is not specified, the initial margin value is used instead.

<a id="options"></a>
### Exchange Options (#options)

There are two types of margin requirements for futures contracts:

  * Initial margin is the amount that must be available on the account at the moment of attempting to enter the market. Further maintenance of the same amount may not be obligatory.
  * Maintenance margin is the minimum amount that must be available on the account for holding a position open.



Both values are specified in the [symbol specification (#specification)](../Market-Watch.md#specification). The final size of the margin depends on the volume:

Volume in lots * Initial margin

Volume in lots * Maintenance margin

If the amount of the maintenance margin is not specified, the initial margin value will be used instead. If neither the initial nor the maintenance margin is specified, the appropriate value will be calculated according to the following formula:

Volume in lots * Contract size * Open market price

The current market Ask price is used for buy deals, while the current Bid price is used for sell deals.

The same calculation method is applied for all risk management modes.

<a id="bonds"></a>
### Exchange Bonds (#bonds)

The bond margin is calculated as part of the position value. Bond prices are provided as a face value percentage, so the position value is calculated as follows:

Volume in lots * Contract size * Face value * Price / 100

The part of the position value to be reserved for maintenance is determined by [margin ratios (#rate)](Margin-Calculation-Retail-Forex-Futures.md#rate).

<a id="forts-futures"></a>
### FORTS Futures (#forts-futures)

The margin for the futures contracts of the Moscow Exchange derivative section is calculated separately for each symbol: First, the margin is calculated for the open position and all Buy orders. Then the margin for the same position and all Sell orders is calculated.

MarginBuy = MarginPos + Sum(MarginBuyOrder)

MarginSell = MarginPos + Sum(MarginSellOrder))

The largest one of the calculated values is used as the final margin value for the symbol.

Thus, the same position is used in the calculation of both values. In the first formula (which includes Buy orders), the position margin is calculated as follows:

MarginPos = Volume * (InitialMarginBuy + (Open Price - SettlementPrice) * Tick Price / Tick Size * (1 + 0.01 * Margin Currency Rate))

The volume is used with a positive sign for long positions and with a negative sign for short positions.

In the second formula (which includes Sell orders), the position margin is calculated as follows:

MarginPos = Volume * (InitialMarginSell + (SettlementPrice - Open Price) * Tick Price / Tick Size * (1 + 0.01 * Margin Currency Rate))

The volume is used with a positive sign for short positions and with a negative sign for long positions.

This approach provides the trader a discount on margin, when there is an open position in the opposite direction with respect to the orders placed (the position acts as collateral for orders).

Margin on orders is calculated by the following formulas:

MarginBuyOrder = Volume * (InitialMarginBuy + (Price - SettlementPrice) * Tick price / Tick size * (1 + 0.01 * Margin currency rate))

MarginSellOrder = Volume * (InitialMarginSell + (SettlementPrice - Price) * Tick price / Tick size * (1 + 0.01 * Margin currency rate))

'Price' here depends on the order time and can be equal to:

  * The Highest and the Lowest price of the contract for the current session is used for not yet executed market or stop Buy and Sell orders, respectively. Since the price is not specified in market orders, the trader is charged the maximum possible margin. Once triggered, stop orders behave similar to market orders.
  * The order price is used for limit orders.
  * The Stop Limit price is used for stop limit orders.



Other parameters in the formulas:

  * InitialMarginBuy — the initial margin for the Buy operation.
  * InitialMarginSell — the initial margin for the Sell operation.
  * Currency margin rate is the rate change radius of the currency, a futures contract is denominated in, relative to the Russian ruble
  * SettlementPrice — settlement price of an instrument for the current session.



All these parameters for calculation are provided by the Moscow Exchange.

> InitialMarginBuy is written to the "Initial margin" field, InitialMarginSell is written to the "Maintenance Margin" field in [symbol properties (#specification)](../Market-Watch.md#specification).

Calculation example

The below example shows the calculation of margin requirements for the following trading account state:

  * Position Buy 3.00 Si-6.18 at 73640
  * Order Buy Limit 2.00 Si-6.18 at 73000
  * Order Sell Limit 10.00 Si-6.18 at 74500



Current session parameters

  * Clearing price = 73638
  * InitialMarginBuy = 7665.41
  * InitialMarginSell = 7739.59
  * Tick price = 1
  * Tick size = 1
  * Margin currency rate = 0



We substitute the values ​​in the formulas

MarginBuy = 3 * (7665.41 + (73640 - 73638) * 1/1) + 2 * (7665.41 + (73000-73638) * 1/1) = 37057.05

MarginSell = -3 * (7739.59 + (73638-73640) * 1/1) +10.0 * (7739.59 + (73638-74500) * 1/1) = 45563.13

Margin = Max(37057.05, 45563.13) = 45563.13

The resulting margin for the Si-6.18 symbol is 45563.13.

<a id="collateral"></a>
### Collateral (#collateral)

Non-tradable instruments of this type are used as trader's assets to provide the [required margin for open positions (#position-list)](../Executing-Trades.md#position-list) of other instruments. For these instruments the margin is not calculated.

<a id="fixed"></a>
### Fixed Margin (#fixed)

If the "Initial margin" field [of the symbol specification (#specification)](../Market-Watch.md#specification) contains any non-zero value, the margin calculation formulas specified above are not applied (except for the calculation of [futures (#futures)](Margin-Calculation-Retail-Forex-Futures.md#futures), as everything remains the same there). In this case, for all types of calculations (except for Forex and Contracts Leverage), the margin is calculated like for the "Futures" calculation type:

Volume in lots * Initial margin

Volume in lots * Maintenance margin

Calculations of the Forex and Contracts Leverage types additionally allow for leverage:

Volume in lots * Initial margin / Leverage

Volume in lots * Maintenance margin / Leverage

> If the amount of the maintenance margin is not specified, the initial margin value is used instead.

<a id="conversion"></a>
## Converting into Deposit Currency (#conversion)

This stage is common for all calculation types. Conversion of the margin requirements calculated using one of the above-mentioned methods is performed in case their currency is different from the account deposit one.

The current exchange rate of a margin currency to a deposit one is used for conversion. The Ask price is used for buy deals, and the Bid price is used for sell deals.

For example, the basic size of the margin previously calculated for buying one lot of EURUSD is EUR 1,000. If the account deposit currency is USD, the current Ask price of EURUSD pair is used for conversion. For example, if the current rate is 1.2790, the total margin size is USD 1,279.

<a id="rate"></a>
## Margin Rate (#rate)

The symbol specification allows setting additional multipliers (rates) for the margin requirements depending on the position/order type.

![Margin Rate](images/specification_margin.png)

The final margin requirements value calculated taking into account the conversion into the deposit currency, is additionally multiplied by the appropriate rate.

For example, the previously calculated margin for buying one lot of EURUSD is USD 1,279. This sum is additionally multiplied by the long margin rate. For example, if it is equal to 1.15, the final margin is 1279 * 1.15 = USD 1470.85.

Margin rates may vary depending on the volume or notional value of positions on the account. In this case, the indication 'Floating' will be displayed next to the block title, followed by the calculation type:

  * Floating: Volume — the total volume of open positions on the account. This calculation is based on the volume of positions for different trading instruments (check with your broker for a detailed list), and not just for the instrument for which you are viewing the specification.
  * Floating: Volume per symbol — the volume of positions for the symbols for which you are viewing the specification.
  * Floating: Notional value — the total value of open positions on the account. This calculation is based on the value of positions for different trading instruments (check with your broker for a detailed list), and not just for the instrument for which you are viewing the specification. The value is calculated based on the position opening price and is converted to the the specified currency at the current conversion rate.
  * Floating: Notional value per symbol — the value of positions for the symbols for which you are viewing the specification. The value is calculated based on the position opening price and is converted to the the specified currency at the current conversion rate.



When you open a position or place an order, the platform checks within which range the position or order falls and applies the appropriate rate.

<a id="spread"></a>
## Calculations for Spread Trading (#spread)

The margin can be charged on preferential basis in case trading positions are in spread relative to each other. The spread trading is defined as the presence of the oppositely directed positions of correlated symbols. Reduced margin requirements provide more trading opportunities for traders. Configuration of spreads is described in a [separate section](Spreads.md).

> Spreads are only used in the [netting (#netting)](../Basic-Principles.md#netting) system for position accounting.

<a id="hedging"></a>
## Calculation in the hedging system of position accounting (#hedging)

If the [hedging (#hedging)](../Basic-Principles.md#hedging) position accounting system is used, the margin is calculated using the same formulas and principles as described above. However, there are some additional features for multiple positions of the same symbol.

<a id="positionsorders-open-in-the-same-direction"></a>
### Positions/orders open in the same direction (#positionsorders-open-in-the-same-direction)

Their volumes are summed up and the weighted average open price is calculated for them. The resulting values are used for calculating margin by the formula corresponding to the [symbol type (#main)](Margin-Calculation-Retail-Forex-Futures.md#main).

For pending orders (if the margin ratio is non-zero) margin is calculated separately.

<a id="opposite-positionsorders"></a>
### Opposite Positions/Orders (#opposite-positionsorders)

Oppositely directed open positions of the same symbol are considered hedged or covered. Two margin calculation methods are possible for such positions. The calculation method is determined by the broker.

Basic calculation | Using the larger leg  
---|---  
Used if "calculate using larger leg" is not specified in the "Hedged margin" field of [contract specification (#specification)](../Market-Watch.md#specification). The calculation consists of several steps:

  * For uncovered volume
  * For covered volume (if hedged margin size is specified)
  * For pending orders

The resulting margin value is calculated as the sum of margins calculated at each step. Calculation for uncovered volume

  * Calculation of the total volume of all positions and market orders for each of the legs — buy and sell.


  * Calculation of the weighted average position and market order open price for each leg: (open price of position or order 1 * volume of position or order 1 + ... + open price of position or order N * volume of position or order N) / (volume of position or order 1 + ... + volume of position or order N).


  * Calculation of uncovered volume (smaller leg volume is subtracted from the larger one).
  * The calculated volume and weighted average price are used then to calculate margin by the appropriate formula corresponding to the [symbol type](Margin-Calculation-Retail-Forex-Futures.md).


  * When considering a [margin ratio (#rate)](Margin-Calculation-Retail-Forex-Futures.md#rate), the larger leg ratio (buy or sell) is used.
  * The weighted average rate value is used when [converting from a margin currency to a deposit one (#conversion)](Margin-Calculation-Retail-Forex-Futures.md#conversion).

Calculation for covered volume Used if the "Hedged margin" value is specified in a [contract specification (#specification)](../Market-Watch.md#specification). In this case margin is charged for hedged, as well as uncovered volume. If the initial margin is specified for a symbol, the hedged margin is specified as an absolute value (in monetary terms). If the initial margin is not specified (equal to 0), the contract size is specified in the "Hedged" field. The margin is calculated by the appropriate formula in accordance with the type of the financial instrument, using the specified contract size. For example, we have two positions Buy EURUSD 1 lot and Sell EURUSD 1 lot, the contract size is 100,000. If the value of 100,000 is specified in the "Hedged field", the margin for the two positions will be calculated as per 1 lot. If you specify 0, no margin is charged for the hedged (covered) volume. Per each hedged lot of a position, the margin is charged in accordance with the value specified in the "Hedged Margin" field in the [contract specification (#specification)](../Market-Watch.md#specification):

  * Calculation of hedged volume for all open positions and market orders (uncovered volume is subtracted from the larger leg).
  * Calculation of the weighted average position and market order open price: (open price of position or order 1 * volume of position or order 1 + ... + open price of position or order N * volume of position or order N) / (volume of position or order 1 + ... + volume of position or order N).
  * The calculated volume, weighted average price and the hedged margin value are used then to calculate margin by the appropriate formula corresponding to the [symbol type](Margin-Calculation-Retail-Forex-Futures.md).


  * When considering a [margin ratio (#rate)](Margin-Calculation-Retail-Forex-Futures.md#rate), the average value of the buy and sell order ratios is used: (Buy rate + Sell rate)/2.
  * The weighted average rate value is used when [converting from a margin currency to a deposit one (#conversion)](Margin-Calculation-Retail-Forex-Futures.md#conversion).

Calculation for pending orders

  * Calculation of margin for each pending order type separately (Buy Limit, Sell Limit, etc.).


  * The weighted average value of the ratio and rate for each pending order type is used when taking into account the [margin ratio (#rate)](Margin-Calculation-Retail-Forex-Futures.md#rate) and [converting margin currency to deposit currency (#conversion)](Margin-Calculation-Retail-Forex-Futures.md#conversion).

Calculation specifics for hedging orders when using fixed margin When an order opposite to an existing position is placed, the margin on the hedged volume is always calculated using the "Hedge margin" value. For the non-hedged volume, the "Initial margin" value is used when placing an order, and "Maintenance margin" is applied after the appropriate position is opened. These calculation specifics only apply for symbols, for which the initial and maintenance margin values are specified (calculation type ["Fixed margin" (#fixed)](Margin-Calculation-Retail-Forex-Futures.md#fixed) or ["Futures" (#futures)](Margin-Calculation-Retail-Forex-Futures.md#futures)). For example, the following parameters are used for EURUSD:

  * Initial margin = 1000
  * Maintenance margin = 500
  * Hedge margin = 500

A trader has a position Buy 1.00 BR-12.18 on a USD account. A margin of 500 USD (as per the "Maintenance margin") is reserved on the trader's account for this position.

  * To open Sell 2.00 BR-12.18, the trader needs the margin of 2000 USD: 500 USD for the existing position, 500 for 1 hedged lot of the new position (in accordance with the "Hedged margin" parameter) and 1000 for 1 non-hedged lot of the new position (as set in the "Initial margin" parameter).
  * Once the position is opened, a margin of 1000 USD will remain reserved on the trader's account: 500 USD for 1 hedged lot (in accordance with "Hedged margin") and 500 USD for 1 non-hedged lot (as specified in the "Maintenance margin").

| Used if "calculate using larger leg" is specified in the "Hedged margin" field of [contract specification (#specification)](../Market-Watch.md#specification).

  * Calculation of margin for shorter and longer legs for all open positions and market orders.
  * Calculation of margin for each pending order type separately (Buy Limit, Sell Limit, etc.).
  * Summing up a longer leg margin: long positions and market orders + long pending orders.
  * Summing up a shorter leg margin: short positions and market orders + short pending orders.


  * The largest one of all calculated values is used as the final margin value.

  
Example The following positions are present:

  * Sell 1 lot at 1.11943
  * Buy 1 lot at 1.11953
  * Sell 1 lot at 1.11943
  * Buy 1 lot at 1.11953
  * Sell 1 lot at 1.11943

Hedged margin size = 100 000. Buy margin rate = 2, for Sell = 4. Leverage = 1:500. Calculate uncovered volume: Sell volume (3) - Buy volume (2) = 1 Calculate the weighted average Open price for the hedged volume by all positions: (1.11943 * 1+1.11953 * 1+1.11943 * 1+1.11953 * 1+1.11943 * 1)/5 = 5.59735/5= 1.11947 Calculate the weighted average Open price for the non-hedged volume by all positions: (1.11943 * 1 + 1.11943 * 1 + 1.11943 * 1)/3 = 1.11943 Calculate the margin ratio for the hedged volume: (buy ratio + sell ratio)/2 = (2 + 4)/2 = 3 The larger leg (sell) margin ratio is used for the non-hedged volume: 4. Calculate the hedged volume margin using the equation: (2.00 lots * 100000 EUR * 1.11947 * 3) / 500 = 1343.36 Calculate the non-hedged volume margin using the equation: (1.00 lot * 100000 EUR * 1.11943 * 4) / 500 = 895.54 The final margin size: 1343.364 + 895.544 = 2238.90 | 
